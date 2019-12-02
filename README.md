# Deployment-
Client/Server
   
    /**
     * @author Luc Nguyen
     * Class: CEN 3024C
     * Profesor: Gossai 
     * <h1> Write a client/server application with two parts, a server and a client.
     * Have client send the server a request to compute whether a number that user
     * provided is prime. Server responds with yes or no, then the client display the answer. 
     * </h1>
     */
     
    import java.io.BufferedReader;
    import java.io.InputStreamReader;
    import java.io.OutputStreamWriter;
    import java.io.PrintWriter;
    import java.net.InetAddress;
    import java.net.Socket;
    
    public class Client {
	
    @SuppressWarnings("resource")
	public static void main(String [] args) throws Exception
    {
    	// Create a socket to connect to the server
        int port = 9000;
        Socket s;
        
        // Create an input stream to receive data from the server
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        
        s = new Socket(InetAddress.getLocalHost(),port);
        
        // Create an output stream to send data to the server
        PrintWriter pw = new PrintWriter(new OutputStreamWriter(s.getOutputStream()));
        
        BufferedReader brl = new BufferedReader(new InputStreamReader(s.getInputStream()));
        
        //Display the user number input
        System.out.print("Enter any number: ");
        
        String str = br.readLine();
        
        pw.println(str);
        pw.flush();
        
        String msg = brl.readLine();
        
        //Print out if user input is prime or not 
        if(msg.equals("true"))
        {
            System.out.println("It is a prime number");
        }
        else
        {
            System.out.println("It is not a prime number");
            }
        }
    }
    
    
    import java.io.*;
    import java.net.*;

    public class Server{

    public static boolean isPrime(int number){
    	
	//Debate if user input number is prime or not
        boolean isPrimeNum = false;
        
        int i = (int) Math.ceil(Math.sqrt(number));
        
        while(i>1)
        {
            if((number != i) && (number % i ==0))
            {
                isPrimeNum = false;
                break;
            }
            else if(!isPrimeNum)
            {
                isPrimeNum = true;
            }
            --i;
        }
        return isPrimeNum;
    }
    
    public static void main(String [] args) throws Exception
    {
    	// Create a server socket
        Socket s;
        int port = 9000;
        
        @SuppressWarnings("resource")
		ServerSocket ss = new ServerSocket(port);
        
        //Printout message waiting for client to run their end
        System.out.println("Waiting for client...");
        
        s = ss.accept();
        
        // Create data input and output streams
        BufferedReader br = new BufferedReader(new InputStreamReader(s.getInputStream()));
        
        PrintWriter pw = new PrintWriter(new OutputStreamWriter(s.getOutputStream()));
        
        int num = Integer.parseInt(br.readLine());
        //Display input from client
        System.out.println("Number sent by client: " + num);
        
        pw.println(Server.isPrime(num));
        pw.flush();
      }
    }



    
    
