# Lab Report 2
## Part 1 - Web Server `ChatServer`
Code for my `ChatServer`: 
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String messages = new String();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("%s", messages.toString());
        } else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            int msgEnd = parameters[1].indexOf("&");
            String msgToAdd = parameters[1].substring(0, msgEnd);
            String userMsg = parameters[2] + ": " + msgToAdd + "\n";
            messages = messages + userMsg;
            return String.format("%s", messages);
        } else {
            return "Please use /add-message?s=MESSAGE&user=USER to add a message.";
        }
    }
}

public class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
<ins>**First Message:**</ins>
![First message sent on ChatServer](lab2Images/chatServerImage1.png) 
1. Which methods in your code are called?
    * The `handleRequest` method was called. 
2. What are the relevant arguments to those methods, and the values of any relevant fields of the **class**?
    * The relevant argument to the `handleRequest` method is the `URI url`, as the method calls `getPath()` on `url` to handle the request given in the URL. The relevant field of the `Handler` class is `String messages`. The value of the field `messages` was an empty `String` at the beginning of the method call.
3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
    * The `messages` field was changed from this request. At the beginning of the method call, it was a blank `String`. However, by the end of the method call, it was changed to contain "kyang: hello everyone" by concatenating the message portion of the request (the part after "s=") and the username (the part after "user="). 

<ins>**Second Message:**</ins>
![Second message sent on ChatServer](lab2Images/chatServerImage2.png)
1. Which methods in your code are called?
    * The `handleRequest` method was called. 
2. What are the relevant arguments to those methods, and the values of any relevant fields of the **class**?
    * The relevant argument to the `handleRequest` method is the `URI url` so that the method can call `getPath()` on it. Again, the relevant field of the `Handler` class is `String messages`. The value of the field `messages` at the beginning of the method call was a `String` containing "kyang: hello everyone". 
3. How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
    * The `messages` field was changed from this request. At the beginning of the method call, it was a `String` containing "kyang: hello everyone". After the method finished running, it was changed to contain "kyang: hello everyone\nAnnouncement: Welcome to the chat server". This was done by concatenating the original value of `messages` with the addition `String` to be added, called `userMsg`. `userMsg` is created by concatenating the message portion of the request and the username given in the request together. 

## Part 2 - SSH Keys
何何
## Part 3 - Something I Learned
何何
