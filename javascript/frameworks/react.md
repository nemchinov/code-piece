1. Использовать PropTypes
    ```javascript
    import PropTypes from 'prop-types';

    class Greeting extends React.Component { }

    Greeting.propTypes = {
        name: PropTypes.string
    };
    // optionalElement: PropTypes.element // A React element
    // optionalMessage: PropTypes.instanceOf(Message)
    // optionalEnum: PropTypes.oneOf(['News', 'Photos'])
    // optionalArrayOf: PropTypes.arrayOf(PropTypes.number)
    // optionalObjectWithShape: PropTypes.shape({
    //   color: PropTypes.string,
    //   fontSize: PropTypes.number
    // })
    // requiredFunc: PropTypes.func.isRequired //  Обязательный параметр
    // requiredAny: PropTypes.any.isRequired

    Greeting.defaultProps = {
        name: 'Stranger'
    };
    ```
2. Отрисовка итерируемых объектов
    ```javascript
    <ul>{names.map(name => <li key={name}> {name} </li>)}</ul>
    ```
3. Hooks (Only Call Hooks at the Top Level, Only Call Hooks from React Functions)
    - useState()
        ```javascript
        function LightBulb() {
            let [light, setLight] = useState(0);
            const setOff = () => setLight(0);
            const setOn = () => setLight(1);

            return (
                <div className="App">
                    <button onClick={setOff}>Off</button>
                    <button onClick={setOn}>On</button>
                </div>
            );
        }
        ```
    - useEffect()
        ```javascript
        function App() {
            let [names, setNames] = useState([]);

            useEffect(() => {
                fetch("https://uinames.com/api/?amount=25&region=nigeria")
                .then(response => response.json())
                .then(data => {
                    setNames(data);
                });
            }, []);// второй аргумент - список переменных для наблюдения и нового обращения к API при изменении, [] - отработать при монтировании

            return (
                <div className="App">
                <div>
                    {names.map((item, i) => (
                    <div key={i}>
                        {item.name} {item.surname}
                    </div>
                    ))}
                </div>
                </div>
            );
        }
        ```
    - useContext()
        ```javascript
        const JediContext = React.createContext();
        //любой потомок может получить это занчение
        function Display() {
            const value = useContext(JediContext);
            return <div>{value}, I am your Father.</div>;
        }
        // присваивание значения
        function App() {
            return (
                <JediContext.Provider value={"Luke"}>
                <Display />
                </JediContext.Provider>
            );
        }
        // В разных файлах
        //context.js
        const JediContext = React.createContext();
        //app.js
        import { JediContext } from './context.js'
        ```
    - useRef()
        ```javascript
        function App() {
            let [name, setName] = useState("Nate");

            let nameRef = useRef();

            const submitButton = () => {
                setName(nameRef.current.value);
            };

            return (
                <div className="App">
                <p>{name}</p>

                <div>
                    <input ref={nameRef} type="text" />
                    <button type="button" onClick={submitButton}>
                    Submit
                    </button>
                </div>
                </div>
            );
        }
        ```
4. High Order Components
5. render props
6. Контекст в React- это способ для дочернего компонента получить доступ к значению в родительском компоненте. При создании React приложения вам часто нужно передавать значения с верха вашего дерева React вниз. Не используя context, вы передаете props через компоненты, которым не обязательно о них знать.
7. 