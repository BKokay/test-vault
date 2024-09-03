---
created: 2024-08-30T10:21
updated: 2024-09-03T11:10
---
# What is flush()?
This is used with `PrintWriter` if you are sending a large amount of data to the client. It ensures that the data is sent to the client immediately. In [[servlet]] the servlet container automatically flushes after the buffer at the end of the request handling the process. 

## When to call flush() manually?
- **Large Data Streams**: If you're sending a large amount of data to the client and want to ensure that the client starts receiving data as soon as possible, you might use `flush()` to send the buffered content partway through processing.
    
- **Real-Time Updates**: For scenarios where you need to push data to the client in real-time (like server-sent events or certain types of streaming responses), using `flush()` can be beneficial.
    
- **Explicit Control**: If you want to ensure that data is sent out at a specific point in your code, rather than waiting for the response to complete, `flush()` gives you that control.
[[java]]