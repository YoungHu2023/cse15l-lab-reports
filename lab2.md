### Part 1 Create ChatServer
My chat server code: 

    import java.io.IOException;
    import java.net.URI
    
    class Handler implements URLHandler {
        // The one bit of state on the server: messages will be displayed by
        // various requests.
        String chat = "";

        public String handleRequest(URI url) {
            if (url.getPath().equals("/")) {
                return "Welcome, please enter your username and message.";
            } else {
                if (url.getPath().contains("/add-message")) {
                    String[] parameters = url.getQuery().split("&");
                    chat += String.format("%s: %s\n",parameters[1].split("=")[1],parameters[0].split("=")[1]);
                    return chat;
                }
            return "404 Not Found!";
            }
        }
    }

    class ChatServer {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }

            int port = Integer.parseInt(args[0]);

            Server.start(port, new Handler());
        }
    }


![Image][chat1.png]  
Methods called:  
- `public String handleRequest(URI url)`:  
      - argument:  
          `/add-message?s=Hello&user=Yang` the path and query part of the URL I typed into the browser.   
      - relevant field: <br>
          `chat`: the concatenated messages on the server. The new message is added to it. 


![Image][chat2.png]  
Methods called:  
- `public String handleRequest(URI url)`:   
      - argument:  <br>
          `/add-message?s=Anybody%20here?&user=Kyle` the path and query part of the URL I typed into the browser.  
      - relevant field:  <br>
          `chat`: the concatenated messages on the server. The new message is added to it. 
Which methods in your code are called?
What are the relevant arguments to those methods, and the values of any relevant fields of the class?
How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.

### Part 2 SSH Keys and Login

### Part 3 What I learned
During these two weeks, I learned many new commands,
