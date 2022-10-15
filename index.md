# Lab Report 2
**Part 1**
```

import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("count")) {
                    num += Integer.parseInt(parameters[1]);
                    return String.format("Number increased by %s! It's now %d", parameters[1], num);
                }
            }
            return "404 Not Found!";
        }
    }
}

class NumberServer {
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
![Screenshot (6)](https://user-images.githubusercontent.com/98442414/195970029-109f4229-c184-41ed-aeaa-9584ef32ff51.png)
In this screenshot, the main and handleRequest methods are called. In this method, the count is increased by one every time it is run and over time increased the count to 12 
![Screenshot (7)](https://user-images.githubusercontent.com/98442414/195970049-d76f7fe1-6473-4e7d-87c6-e2269a0dd08b.png)
In this screenshot, the main and handleRequest methods are called. The query in this was not valid which is why it returned a NullPointerException method. 
![Screenshot (8)](https://user-images.githubusercontent.com/98442414/195970059-9a0a3b4c-7906-4ebd-9756-66c903ef9976.png)
In this screenshot, the main and handleRequest methods are called. The count was set to 12 which is why it prints that the number is equal to 12

**Part 2:** 

A bug in reverseInPlace is that it reverses over itself and then reverses again, therefore undoing what the method was supposed to do. The bug in averageWithoutLowest is that it will skip over several elements if they are all the lowest. 
Due to this, reverseInPlace does nothing and averageWithoutLowest returns an average that is too high
In order to fix this, reverseInPlace needs to be switched so it stops reversing after reaching the middlepoint in the array and averageWithoutLowest needs to subtract the lowest from the sum of all numbers rather than removing it before summing it up. 
