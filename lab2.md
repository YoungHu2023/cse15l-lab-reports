### Part 1 Create ChatServer
My chat server code: 

'''

    import java.io.IOException;
    import java.net.URI
    
    class Handler implements URLHandler {
        // The one bit of state on the server: messages will be displayed by
        // various requests.
        String username;
        String chat = "";
        String msg;

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
'''

### Part 2 SSH Keys and Login

### Part 3 What I learned
