# Examples of `MessageChannel` usage

## Navigation

- [Example 1](#example-1)
- [Example 2](#example-2)
- [Example 3](#example-3)
- [Example 4](#example-4)
- [Example 5](#example-5)

## Example 1

**Источник**: <https://github.com/umijs/umi/blob/9d160fc2bc9236b3df06e349412bbe0a6b2df451/examples/ant-design-pro/src/global.tsx#L41>

```TypeScript

await new Promise((resolve, reject) => {
  const channel = new MessageChannel();
  channel.port1.onmessage = (msgEvent) => {
    if (msgEvent.data.error) {
      reject(msgEvent.data.error);
    } else {
      resolve(msgEvent.data);
    }
  };
  worker.postMessage({ type: 'skip-waiting' }, [channel.port2]);
});

```

## Example 2

**Источник**: <https://github.com/rhysmorgan134/react-carplay/blob/1f52e18526b830734987a388911673d553931111/src/renderer/src/components/Carplay.tsx#L20>

```TypeScript
const videoChannel = new MessageChannel()

// ...
// Some code
// ...

worker.postMessage(new InitEvent(canvas, videoChannel.port2), [
      canvas,
      videoChannel.port2,
])

```

## Example 3

**Источник**: <https://github.com/audio-node/web-noise/blob/439f9ab8aabb05e8f416825900f5e4353406f90d/packages/base-nodes/src/ValueMeter/ValueMeter.tsx#L40-L43>

```TypeScript

const channel = new MessageChannel();
channel.port2.start();

audioNode.registerPort(channel.port1);

// ...
// Some code
// ...

channel.port2.addEventListener("message", handler);

```

## Example 4

**Источник**: <https://github.com/GoogleChrome/workbox/blob/f4a49dac92d043926505c83a02ebeea5c5bf1957/packages/workbox-window/src/messageSW.ts#L27-L35>

```TypeScript

function messageSW(sw: ServiceWorker, data: {}): Promise<any> {
  return new Promise((resolve) => {
    const messageChannel = new MessageChannel();
    messageChannel.port1.onmessage = (event: MessageEvent) => {
      resolve(event.data);
    };
    sw.postMessage(data, [messageChannel.port2]);
  });
}

```

## Example 5

**Источник**: <https://github.com/elastic/kibana/blob/910a806aab5f4c76a6fd7e6ae84b3d51704560a0/x-pack/plugins/screenshotting/server/formats/pdf/pdf_maker/pdfmaker.ts#L207-L243>

```TypeScript

try {
  return await new Promise<Uint8Array>((resolve, reject) => {
    const { port1: myPort, port2: theirPort } = new MessageChannel();
    this.worker = this.createWorker(theirPort);
    this.worker.on('error', (workerError: NodeJS.ErrnoException) => {
      if (workerError.code === 'ERR_WORKER_OUT_OF_MEMORY') {
        reject(new errors.PdfWorkerOutOfMemoryError(workerError.message));
      } else {
        reject(workerError);
      }
    });
    this.worker.on('exit', () => {});


    // We expect one message from the worker generating the PDF buffer.
    myPort.on('message', ({ error, data }: GeneratePdfResponse) => {
      if (error) {
        reject(new Error(`PDF worker returned the following error: ${error}`));
        return;
      }
      if (!data) {
        reject(new Error(`Worker did not generate a PDF!`));
        return;
      }
      this.pageCount = data.metrics.pages;
      resolve(data.buffer);
    });


    // Send the request
    const generatePdfRequest: GeneratePdfRequest = {
      data: this.getGeneratePdfRequestData(),
    };
    myPort.postMessage(generatePdfRequest, this.transferList);
  });
} finally {
  await this.cleanupWorker();
}
}

```
