# Node.js Server Hang Issue

This repository demonstrates a bug in a Node.js HTTP server where it hangs after receiving multiple requests with significant response delays.  The server becomes unresponsive to new requests until the delayed responses are finally sent.

## Bug Description

The server uses `setTimeout` to simulate a 5-second delay in sending the response.  If multiple requests are made within this delay period, the server appears to hang, and new requests are not processed.

## How to Reproduce

1. Clone this repository.
2. Run `node bug.js` to start the server.
3. Send multiple requests to `http://localhost:3000` using a tool like `curl` or a web browser.
4. Observe that after a few requests, the server becomes unresponsive.

## Solution

The solution uses the `async/await` syntax and promises to handle the requests concurrently without blocking the event loop, avoiding the hang issue. The `bugSolution.js` file shows the correct implementation.

## Additional Notes

This bug is commonly caused by blocking the Node.js event loop for extended periods, particularly within request handlers. Using async operations and avoiding synchronous, long-running tasks in request handlers is crucial for maintaining responsiveness.