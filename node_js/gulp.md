# [Gulp](https://gulpjs.com/docs/en/getting-started/quick-start)

1. Install
    ```javascript
    npm install gulp-cli -g
    npm install gulp -D
    npx -p touch nodetouch gulpfile.js
    ```
1. Using `gulp <task> <othertask>`

# New
1. Naming: gulpfile.js, Gulpfile.js, gulpfile.ts, gulpfile.babel.js
1. Splitting a gulpfile: Each task can be split into its own file, then imported into your gulpfile for composition
    > Node's module resolution allows you to replace your gulpfile.js file with a directory named gulpfile.js that contains an index.js file which is treated as a gulpfile.js. This directory could then contain your individual modules for tasks.
1. Public tasks are exported from your gulpfile / Private tasks are made to be used internally
    ```javascript
    const { series } = require('gulp');

    function clean(cb) {
        cb();
    }

    function build(cb) {
        cb();
    }

    exports.build = build;
    exports.default = series(clean, build);
    ```
1. `gulp --tasks`
1. Compose tasks
    * series `exports.build = series(transpile, bundle);`
    * parallel `exports.build = parallel(javascript, css);`
    * condition 
        ```javascript
        if (process.env.NODE_ENV === 'production') {
            exports.build = series(transpile, minify);
        } else {
            exports.build = series(transpile, livereload);
        }
        ```
    * nested 
        ```javascript
        exports.build = series(
            clean,
            parallel(
                cssTranspile,
                series(jsTranspile, jsBundle)
            ),
            parallel(cssMinify, jsMinify),
            publish
        );
        ```
1. Signal task completion
    ```javascript
        //stream
        const { src, dest } = require('gulp');
        function streamTask() {
            return src('*.js')
                .pipe(dest('output'));
        }
        exports.default = streamTask;
        //promise
        function promiseTask() {
            return Promise.resolve('the value is ignored');
        }
        exports.default = promiseTask;
        //
    ```
1. Example
    ```javascript
    const { src, dest } = require('gulp');
    const babel = require('gulp-babel');
    const uglify = require('gulp-uglify');

    exports.default = function() {
        return src('src/*.js')
            .pipe(babel())
            .pipe(src('vendor/*.js'))
            .pipe(uglify())
            .pipe(dest('output/'));
    };
    ```
1. Watch: 'add', 'addDir', 'change', 'unlink', 'unlinkDir', 'ready', 'error', 'all'
    ```javascript
    const { watch } = require('gulp');

    // All events will be watched
    watch('src/*.js', { events: 'all' }, function(cb) {
        // body omitted
        cb();
    });
    ```
    Initial execution: `watch('src/*.js', { ignoreInitial: false }, function(cb) {...`
    Queueing: `watch('src/*.js', { queue: false }, function(cb) {...` - The task will be run (concurrently) for every change made
    Delay: `watch('src/*.js', { delay: 500 }...`

# Old
1. Gulpfile (`gulpfile.js`)
    ```javascript
       const gulp = require('gulp');
       // Таск - инструкция: gulp mytask
       gulp.task('mytask', function() {
            console.log('Привет, я таск!');
        });
    ```
    Пример:
    ```javascript
    npm i gulp-sass --save-dev
    //gulpfile
    let gulp = require('gulp'),
        sass = require('gulp-sass');
    
    gulp.task('sass', function() { // Создаем таск "sass"
        return gulp.src('app/sass/main.sass') // Берем источник: **/*.sass
            .pipe(sass()) // Преобразуем Sass в CSS посредством gulp-sass
            .pipe(gulp.dest('app/css')) // Выгружаем результата в папку app/css
    });
    ```
1. Glob, шаблоны выборки
    * `*.sass` все файлы в корневой папке
    * `**/*.js` все файлы во всех папках проекта
    * `!header.sass` исключает файл из общей выборки (['script/**/*.js', '!scripts/vendor/'])
    * `*.+(scss|sass)` шаблон
    ```javascript
    gulp.task('sass', function(){
        return gulp.src('app/sass/**/*.sass') // Берем все sass файлы из папки sass и дочерних, если таковые будут
            .pipe(sass())
            .pipe(gulp.dest('app/css'))
    });
    ```
1. Watch
    ```javascript
    gulp.watch('watch-files', ['task1', 'task2']); 
    // example
    gulp.watch('app/sass/**/*.sass', ['sass']);
    // gulp watch
    gulp.task('watch', function() {
        gulp.watch('app/sass/**/*.sass', ['sass']); // Наблюдение за sass файлами
        // Наблюдение за другими типами файлов
    });
    ```
1. LiveReload
    ```javascript
    npm i browser-sync --save-dev
    // gulpfile
    let gulp = require('gulp'),
        sass = require('gulp-sass'),
        browserSync = require('browser-sync'); // Подключаем Browser Sync
    
    gulp.task('browser-sync', function() {
        browserSync({
            server: {
                baseDir: 'app' // Директория для сервера - app
            },
            notify: false // Отключаем уведомления
        });
    });
    gulp.task('sass', function(){
        return gulp.src('app/sass/**/*.sass')
            .pipe(sass())
            .pipe(gulp.dest('app/css'))
            .pipe(browserSync.reload({stream: true})) // Обновляем CSS на странице при изменении
    });
    gulp.task('watch', ['browser-sync', 'sass'], function() {
        gulp.watch('app/sass/**/*.sass', ['sass']);
        gulp.watch('app/*.html', browserSync.reload); // Наблюдение за HTML файлами в корне проекта
        gulp.watch('app/js/**/*.js', browserSync.reload); // Наблюдение за JS файлами в папке js
    });
    ```
1. Build and minification
    ```javascript
    npm i --save-dev gulp-concat gulp-uglifyjs gulp-cssnano gulp-rename del
    // gulpfile
    let  gulp = require('gulp'),
        concat = require('gulp-concat'), // для конкатенации файлов
        uglify = require('gulp-uglifyjs'), // для сжатия JS
        cssnano = require('gulp-cssnano'), // для минификации CSS
        rename = require('gulp-rename'), // для переименования файлов
        del = require('del'); // для удаления файлов и папок

    gulp.task('scripts', function() {
        return gulp.src([
            'app/libs/jquery/dist/jquery.min.js',
            'app/libs/magnific-popup/dist/jquery.magnific-popup.min.js'
        ])
            .pipe(concat('libs.min.js')) // Собираем их в кучу в новом файле libs.min.js
            .pipe(uglify()) // Сжимаем JS файл
            .pipe(gulp.dest('app/js')); // Выгружаем в папку app/js
    });
    gulp.task('css-libs', ['sass'], function() {
        return gulp.src('app/css/libs.css')
            .pipe(cssnano())
            .pipe(rename({suffix: '.min'}))
            .pipe(gulp.dest('app/css'));
    });

    gulp.task('clean', function() {
        return del.sync('dist'); // Удаляем папку dist перед сборкой
    });

    gulp.task('build', ['clean', 'sass', 'scripts', 'css-libs'], function() {
        let buildCss = gulp.src([ // Переносим CSS стили
            'app/css/main.css',
            'app/css/libs.min.css'
            ]).pipe(gulp.dest('dist/css'))

        let buildFonts = gulp.src('app/fonts/**/*') // Переносим шрифты
            .pipe(gulp.dest('dist/fonts'))

        let buildJs = gulp.src('app/js/**/*') // Переносим скрипты
            .pipe(gulp.dest('dist/js'))

        let buildHtml = gulp.src('app/*.html') // Переносим HTML
            .pipe(gulp.dest('dist'));
    });
    ```
1. Images
    ```javascript
    npm i gulp-imagemin imagemin-pngquant gulp-cache --save-dev
    //gulpfile
    let imagemin = require('gulp-imagemin'),
        pngquant = require('imagemin-pngquant'),
        cache = require('gulp-cache');
    
    gulp.task('img', function() {
        return gulp.src('app/img/**/*') // Берем все изображения из app
            .pipe(cache(imagemin({ // Сжимаем их с наилучшими настройками
                interlaced: true,
                progressive: true,
                svgoPlugins: [{removeViewBox: false}],
                use: [pngquant()]
            })))
            .pipe(gulp.dest('dist/img')); // Выгружаем на продакшен
    });
    ```
1. Autoprefix
    ```javascript
    npm i --save-dev gulp-autoprefixer
    //gulpfile
    let autoprefixer = require('gulp-autoprefixer');

    gulp.task('sass', function(){ // Создаем таск Sass
        return gulp.src('app/sass/**/*.sass') // Берем источник
            .pipe(sass()) // Преобразуем Sass в CSS посредством gulp-sass
            .pipe(autoprefixer(['last 15 versions', '> 1%', 'ie 8', 'ie 7'], { cascade: true })) // Создаем префиксы
            .pipe(gulp.dest('app/css')) // Выгружаем результата в папку app/css
            .pipe(browserSync.reload({stream: true})) // Обновляем CSS на странице при изменении
    });
    ```
1. Default `gulp.task('default', ['watch']);` ~ `gulp`
1. Clear cache `gulp.task('clear', function () { return cache.clearAll(); })`
1. Linter 
    ```javascript
    npm install gulp-jshint --save-dev
    //gulpfile
    let jshint = require("gulp-jshint");
    gulp.task("lint", function() {
        return gulp.src("src/js/*.js")
            .pipe(jshint())
            .pipe(jshint.reporter("default"));
    });
    ```