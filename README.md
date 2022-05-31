# Password.java
import java.util.*;
import java.text.*;
import java.io.*;
public class Password{
        public static boolean check(String a,String b)
        {
          int x=Integer.parseInt(a.substring(0,2));
          int y=Integer.parseInt(b.substring(0,2));
	  int z=x-y;
          //System.out.println("z value is "+z);
          if(y-x>=1)
          {
             return true;
          }
          else
          {
            int p=Integer.parseInt(a.substring(3,5));
            int q=Integer.parseInt(b.substring(3,5));
	    int r=q-p;
	    //System.out.println("r value is "+r);
            if(q-p>=1)
            {
              return true;
            }
            else
            {
              int m=Integer.parseInt(a.substring(6,8));
              int n=Integer.parseInt(b.substring(6,8));
	      int o=n-m;
	      //System.out.println("o value is "+o);
              if(n-m>=1)
              {
                return true;
              }
            }
          }
         return false;
        }
	public static void main(String args[])
	{
          String path="C:\\Users\\";
  	  System.out.println("welcome to login page");
	  System.out.println("if you have already has an account enter yes else no to create");
          Scanner sc=new Scanner(System.in);
          String ch=sc.nextLine();
          System.out.println("ch is "+ch);
          if(ch.equals("yes"))
          {
            int fop=1,m=0,wrong=0;
            while(fop==1)
            {
	    	System.out.println("enter your login id");
            	String sfile=sc.nextLine();
                sfile=sfile+".txt";
                try
                {
	    		File tmp = new File(sfile);
	    		boolean exists = tmp.exists();
                	if(exists==true)
                	{
				int store=1;
				fop=0;
 				int p=1;
				String gotpass="";
                                String gotdate="";
                    		Scanner scan=new Scanner(tmp);
                                int d=0;
                    		while(scan.hasNextLine())
                    		{
                       		  d++;
                                  if(d==1)
                                  {
                                    gotpass=gotpass+scan.nextLine();
                                  }
                                  if(d==2)
                                  {
                                    p=Integer.parseInt(scan.nextLine());
                                  }
                                  if(d==3)
                                  {
                                    gotdate=gotdate+scan.nextLine();
                                  }
                                }
				store=p;
				//System.out.println("p value is "+p);
				//System.out.println("gotpass "+gotpass);
				//System.out.println("gotdate "+gotdate);
                                scan.close();
                                int find=0;
                                if(p>=6)
                                {
				   DateFormat dl=new SimpleDateFormat("yy/MM/dd");
				   Date date=new Date();
                                   String cdate=dl.format(date);
				   //System.out.println("current date "+cdate);
                                   if(check(gotdate,cdate)==true)
                                   {
                                     p=1; 
                                   }
				}
				if(p>=6)
				{
                                  System.out.println("you have already tried ur pasword for 5 times which are wrong please try after one day");
                                }
                                else
				{
                    		while(p<=5 && find==0)
                    		{
            				System.out.println("enter the password");
	    				String passlog=sc.nextLine();
            				String passlogtemp="";
            				for(int j=0;j<passlog.length();j++)
	    				{
						int ascii=(int)passlog.charAt(j);
                				ascii=(ascii%10)+(ascii+1)%10+(ascii*3)%5;
						passlogtemp=passlogtemp+String.valueOf(ascii);
            				}
	    				//System.out.println("passlog is "+passlog);
            				//System.out.println("passlogtemp is "+passlogtemp);
                                        if(gotpass.equals(passlogtemp))
                                        {
                                           find=1;
                                        }
                                        else
                                        {
                                           p++;
					   int chances=6-p;
					   System.out.println("entered wrong password you have only"+" "+chances+" "+"chances"+" "+"remanining"); 
            			           //System.out.println("p value is "+p);
                                        }
	  	    		}
				if(p>5 && find==0)
                                {
                                  System.out.println("you have entered 5 times wrong password try after 1 day"); 
				  Scanner scann=new Scanner(tmp);
				  String oldtext="";
                                  while(scann.hasNextLine())
                                  {
				    oldtext=oldtext+scann.nextLine()+System.lineSeparator();
				  }
				   //System.out.println("oldtext is "+oldtext);
				   DateFormat dld=new SimpleDateFormat("yy/MM/dd");
				   Date date=new Date();
                                   String cudate=dld.format(date);
                                   //String newtext=oldtext.replaceAll(gotdate,cudate);
				   
				   String newtext=oldtext.replaceAll(String.valueOf(store),"6");
				   FileWriter writer=new FileWriter(sfile);
				   writer.write(newtext);
                                   writer.close(); 
				  //System.out.println(""+newtext);
                                }
                                else
                                {
                                   System.out.println("you are logged in");
                                }
				}
			}
			else
			{
					wrong++;
					if(wrong==5)
					{
					    System.out.println("please try to login after sometime");
					    return;
					}
                           System.out.println("you have entered the wrong username");
			   System.out.println("enter correct username");
                        }
              	}
                catch(IOException e)
                {
                    e.printStackTrace();
                }
             }
	  }
          else
	  {
            while(ch.equals("no")) 
            {
	      int i=0;
              int u=1;
              String username="";
              while(u==1)
              {
                System.out.println("enter a user name to create account");
                String exusername=sc.nextLine();
                exusername=exusername+".txt";
                try 
		{
      		   File myObj = new File(exusername);
      		   if (myObj.createNewFile()) 
		   {
                     u=0;
                     username=username+exusername;
        	     System.out.println("username created: " + myObj.getName());
      		   } 
		   else 
		   {
         	     System.out.println("username already taken try another");
      		   }
    		} 
		catch (IOException e) 
		{
      		   System.out.println("An error occurred try again");
      		   e.printStackTrace();
    		}
              }
	      System.out.println("enter password for the account");
              System.out.println("note the password must contain a character");
	      System.out.println(" and it must not contains three consecutive same letters ");
	      int f=1;
              String password="";
              while(f==1)
              {
	        String example=sc.nextLine();
                char x=example.charAt(0);
                int count=0;
                int flag=0;
                HashSet<Integer>set=new HashSet<Integer>();
                for(int k=0;k<example.length();k++)
                {
                  int ascii=(int)example.charAt(k);
                  set.add(ascii);
                  if(example.charAt(k)==x)
                  {
                    count++;
                    if(count>=3)
                    {
                      flag=1;
                      break;
                    }
                  }
                  else
                  {
                    x=example.charAt(k);
                    count=1;
                  } 
                }
                if(flag==0 && (set.contains(36) || set.contains(64) || set.contains(95)))
                {
                  password=password+example;
                  f=0;
                } 
                else
                {
	          if(flag==1)
                  {
                   System.out.println("enter  new password as it contains three consecutive letters");
                  }
                  else
                  {
                    System.out.println("enter new password as it does not contain a character");
                  }
                }  
              }
	      String passwordtemp="";
	      for(int j=0;j<password.length();j++)
	      {
		int ascii=(int)password.charAt(j);
                ascii=(ascii%10)+(ascii+1)%10+(ascii*3)%5+'a';
		passwordtemp=passwordtemp+String.valueOf(ascii);
              }
	      try 
              {
      		FileWriter myWriter = new FileWriter(username);
      		myWriter.write(passwordtemp+"\n");
                //myWriter.append("\n");
		myWriter.write("1"+"\n");
                DateFormat df = new SimpleDateFormat("yy/MM/dd");
       		Date dateobj = new Date();
       		String datime=df.format(dateobj);
                myWriter.write(datime);
      		myWriter.close();
      		System.out.println("account created successfully");
    	      } 
	      catch (IOException e) 
	      {
      		System.out.println("An error occurred.");
      		e.printStackTrace();
    	      }
              /*try  
	      {  
		File read=new File(username);       
		Scanner readscan=new Scanner(read);       
		while(readscan.hasNextLine())  
		{  	
		  System.out.println(readscan.nextLine());  
                  System.out.println("");     
		}  
		readscan.close();       
	      }  
	      catch(IOException e)  
	      {  
		e.printStackTrace();  
	      }*/  
              //System.out.println("account created");
              ch=ch+"123";
          }
        }
      }
 }
