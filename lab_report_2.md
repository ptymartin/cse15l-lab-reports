```
import java.io.IOException;
import java.net.URI;

class ChatHandler implements URLHandler {
    String s = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return s;
        } else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            String[] splitParams = parameters[1].split("&");
            s = s + String.format("%s : %s", parameters[2], splitParams[0]) + '\n';
            return s;
        } else { return "404 Not Found!"; }
        }
    }

    class ChatServer {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }
    
            int port = Integer.parseInt(args[0]);
    
            Server.start(port, new ChatHandler());
        }
    }
```

![add_message1](add_message1.png)
The first method called by this is ```handleRequest()``` in the ```ChatHandler``` class. This then calls ```url.getPath().contains()```, ```url.getQuery().split()``` and ```parameters[1].split()```. Finally the string is added and the output is formatted with ```String.format()```. The relevant argument for ```handleRequest()``` is the url. The relevant argument for ```url.getPath().contains()``` is ```"/add-message"```. The relevant arguments for ```url.getQuery().split()``` and ```parameters[1].split()``` are ```"="``` and ```"&"``` respectively. For ```String.format()```, ```parameters[2]``` and ```splitParams[0]``` are the outputs that get formatted and concatenated.


![add_message2](add_message2.png)


