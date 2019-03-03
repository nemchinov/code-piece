1. `worker_threads` - создание потоков выполнения кода на основе воркеров
1.  `SharedArrayBuffer` - создание разделяемой памяти для различных потоков

```javascript
const { Worker } = require('worker_threads')

function runService(workerData) {
  return new Promise((resolve, reject) => {
    const worker = new Worker('./service.js', { workerData });
    worker.on('message', resolve);
    worker.on('error', reject);
    worker.on('exit', (code) => {
      if (code !== 0)
        reject(new Error(`Worker stopped with exit code ${code}`));
    })
  })
}

// worker
const { workerData, parentPort } = require('worker_threads')

// Тут, асинхронно, не блокируя главный поток,
// можно выполнять тяжёлые вычисления.

parentPort.postMessage({ hello: workerData })
```

