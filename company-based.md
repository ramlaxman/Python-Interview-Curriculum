#### GS Lab
  - How will you sort result of student whose marks are unknown to 
    you based on their roll numbers?
   Using bubble sort.

#### Webonise labs
  
  - **How will you measure memory on Linux server?**
    - 1. free command
    
        The free command is the most simple and easy to use command to check memory usage on linux:
    
        `$ free -m`

        total  used  free   shared  buffers  cached
        Mem:  7976  6459   1517  0   865     2248
        -/+ buffers/cache:       3344       4631
        Swap:         1951          0       1951

        The m option displays all data in MBs. The second line tells that 4.6 GB is free. This is the free memory in first line added with the buffers and cached amount of memory. Linux has the habit of caching lots of things for faster performance, so that memory can be freed and used if needed. The last line is the swap memory, which in this case is lying entirely free.

    - 2. /proc/meminfo

        Know that the /proc file system does not contain real files. They are rather virtual files that contain dynamic information about the kernel and the system.
        
        >`$ cat /proc/meminfo`   
        MemTotal:        8167848 kB     
        MemFree:         1409696 kB     
        Buffers:          961452 kB     
        Cached:          2347236 kB     
        SwapCached:            0 kB     
        Active:          3124752 kB

        Check the values of MemTotal, MemFree, Buffers, Cached, SwapTotal, SwapFree.
        They indicate same values of memory usage as the free command.

    - 3. vmstat
        
        The vmstat command with the s option, lays out the memory usage statistics much like the proc command. Here is an example
        <Use one tab and enter to make block of multiple lines>
        
        >`$ vmstat -s`       
        8167848 K total memory  
        7449376 K used memory   
        3423872 K active memory     
        3140312 K inactive memory   
        718472 K free memory    
        1154464 K buffer memory     
        2422876 K swap cache    
        1998844 K total swap    
        0 K used swap   
        1998844 K free swap     
        392650 non-nice user cpu ticks      
        
        8073 nice user cpu ticks        
        
            83959 system cpu ticks
        
            10448341 idle cpu ticks
        
        91904 IO-wait cpu ticks
        
            0 IRQ cpu ticks
        
            2189 softirq cpu ticks
        
            0 stolen cpu ticks
        
        2042603 pages paged in
        
        2614057 pages paged out
        
            0 pages swapped in
        
            0 pages swapped out
                
        42301605 interrupts
        
        94581566 CPU context switches
        
        1382755972 boot time
        
            8567 forks
        
        The top few lines indicate total memory, free memory etc and so on.
    
    - 4. *top* command
        
        The top command is generally used to check memory and cpu usage per process. However it also reports total memory usage and can be used to monitor the total RAM usage. The header on output has the required information. Here is a sample output:
        
        top - 15:20:30 up  6:57,  5 users,  load average: 0.64, 0.44, 0.33
        
        Tasks: 265 total,   1 running, 263 sleeping,   0 stopped,   1 zombie
        
        %Cpu(s):  7.8 us,  2.4 sy,  0.0 ni, 88.9 id,  0.9 wa,  0.0 hi,  0.0 si,  0.0 st

        KiB Mem:   8167848 total,  6642360 used,  1525488 free,  1026876 buffers
        
        KiB Swap:  1998844 total,        0 used,  1998844 free,  2138148 cached

        PID USER      PR  NI  VIRT  RES  SHR S  %CPU %MEM    TIME+  COMMAND

        2986 enlighte  20   0  584m  42m  26m S  14.3  0.5   0:44.27 yakuake
        
        1305 root      20   0  448m  68m  39m S   5.0  0.9   3:33.98 Xorg
        
        7701 enlighte  20   0  424m  17m  10m S   4.0  0.2   0:00.12 kio_thumbnail

        Check the KiB Mem and KiB Swap lines on the header. They indicate total, used and free amounts of the memory. The buffer and cache information is present here too, like the free command.

    - 5. *htop*
        
        Similar to the top command, the htop command also shows memory usage along with various other details.

        The header on top shows cpu usage along with RAM and swap usage with the corresponding figures. 
        
        **RAM Information**
        
        To find out hardware information about the installed RAM, use the demidecode command. It reports lots of information about the installed RAM memory.

        >`$ sudo dmidecode -t 17`    
        `# dmidecode 2.11`
        *SMBIOS 2.4 present.*   
        Handle 0x0015, DMI type 17, 27 bytes    
        Memory Device   
        Array Handle: 0x0014    
        Error Information Handle: Not Provided  
        Total Width: 64 bits    
        Data Width: 64 bits 
        Size: 2048 MB   
        Form Factor: DIMM   
        Set: None   
        Locator: J1MY   
        Bank Locator: CHAN A DIMM 0     
        Type: DDR2  
        Type Detail: Synchronous    
        Speed: 667 MHz  
        Manufacturer: 0xFF00000000000000    
        Serial Number: 0xFFFFFFFF   
        Asset Tag: Unknown  
        Part Number: 0x524D32474235383443412D36344643FFFFFF
        
        Provided information includes the size (2048MB), type (DDR2) , speed(667 Mhz) etc.

  - **How will you check memory leak on Linux?**
    - valgrind along with gcc.

  - **What are parameters to consider for checking when server is down?**
    - Server A Can’t Talk to Server B 
        - Client or Server Problem                          
          To go to another host on the same network and try to access the server.
        - Is It Plugged In?          
          You first want to verify that your client’s connection to the network is healthy. To do this you can use the ethtool program (installed via the ethtool package) to verify that your link is up (the Ethernet device is physically connected to the network). 
        
          If you aren’t sure what interface you use, run the `/sbin/ifconfig` command to list all the available network interfaces and their settings. So if your Ethernet device was at eth0 
          
          `$ sudo ethtool eth0`
        
          >Settings for eth0:   
          Link detected: yes
        
          Here, on the final line, you can see that Link detected is set to yes, so dev1 is physically connected to the network. If this was set to no, you would need to physically inspect dev1’s network connection and make sure it was connected. Since it is physically connected, you can move on.

        - Is the Interface Up? 
        
          Once you have established that you are physically connected to the network, the next step is to confirm that the network interface is configured correctly on your host. The best way to check this is to run the `ifconfig` command with your interface as an argument. So to test eth0’s settings

          `$ sudo ifconfig eth0`
         
          If the interface is not configured, try running 
          
          `sudo ifup eth0` and then run `ifconfig` again to see if the interface comes up. 
          
          If the settings are wrong or the interface won’t come up, inspect `/etc/network/interfaces` on Debian-based systems or `/etc/sysconfig/ network_scripts/ifcfg-eth0` on Red Hat-based systems. 
          
          It is in these files that you can correct any errors in the network settings. Now if the host gets its IP through DHCP, you will need to move your troubleshooting to the DHCP host to find out why you aren’t getting a lease.
            
        - Is It on the Local Network?

          The route command will display your current routing table, including your default gateway:

          `$ sudo route -n`

          `$ sudo service network restart`

          `$ ping -c 5 10.1.1.1`
        
        - Is DNS Working?
        
          Once you have confirmed that you can speak to the gateway, the next thing to test is whether DNS functions. Both the nslookup and dig tools can be used to troubleshoot DNS issues, but since you need to perform only basic testing at this point, just use nslookup to see if you can resolve web1 into an IP:
            
          `$ nslookup web1`

          DNS is working. The web1 host expands into web1.example.net and resolves to the address 10.1.2.5. Of course, make sure that this IP matches the IP that web1 is supposed to have! In this case, DNS works, however, there are also a number of ways DNS could fail.
          
          - No Name Server Configured or Inaccessible Name Server 
          
          If you see the following error, it could mean either that you have no name servers configured for your host or they are inaccessible: 
          
          >`$ nslookup web1`     
          ;; connection timed out; no servers could be reached
          
          In either case you will need to inspect /etc/resolv.conf and see if any name servers are configured there. If you don’t see any IP addresses configured there, you will need to add a name server to the file. Otherwise, if you see something like the following, you need to start troubleshooting your connection with your name server starting off with ping:
          
          search example.net    
          nameserver 10.1.1.3

          If you can’t ping the name server and its IP address is in the same subnet (in this case, 10.1.1.3 is within the subnet), the name server itself could be completely down. If you can’t ping the name server and its IP address is in a different subnet, then skip ahead to the Can I Route to the Remote Host? section, 
          but only apply those troubleshooting steps to the name server’s IP.
          If you can ping the name server but it isn’t responding, skip ahead to the
          Is the Remote Port Open? section.
          
          - Missing Search Path or Name Server Problem          
          
          It is also possible that you will get the following error for your nslookup command:
            
          `$ nslookup web1`
          > Server: 10.1.1.3    
          Address: 10.1.1.3#53      
          **server can’t find web1: NXDOMAIN

          Here you see that the server did respond, since it gave a response: server can’t find web1. This could mean two different things. One, it could mean that web1’s domain name is not in your DNS search path. This is set in /etc/resolv.conf in the line that begins with search. A good way to test this is to perform the same nslookup command, only use the fully qualified domain name (in this case, web1.example.net). If it does resolve, then either always use the fully qualified domain name, or if you want to be able to use just the hostname, add the domain name to the search path in /etc/resolv.conf. If even the fully qualified domain name doesn’t resolve, then the problem is on the name server. If the name server is supposed to have that record, then that zone’s configuration needs to be examined. If it is a recursive name server,then you will have to test whether or not recursion is working on the name server by looking up some other domain. If you can look up other domains, then you must check if the problem is on the remote name server that does contain the zones.
        
        - Can I Route to the Remote Host?
          
            traceroute  

        - Is the Remote Port Open? 
            
            port 80. The next test is to see whether the port is even open.   
            `$ telnet 10.1.2.5 80`
            
            If nmap isn’t installed, use your package manager to install the nmap package. To test web1:  
            `$ nmap -p 80 10.1.2.5`

            nmap is smart enough that it can often tell the difference between a closed port that is truly closed and a closed port behind a firewall. Normally when a port is actually down, nmap will report it as closed. Here it reported it as filtered. What this tells us is that some firewall is in the way and is dropping the packets to the floor. This means you need to investigate any firewall rules on the gateway (10.1.1.1) and on web1 itself to see
            if port 80 is being blocked.

        - Test the Remote Host Locally
            
            At this point, we have either been able to narrow the problem down to a network issue or we believe the problem is on the host itself, we can do a few things to test whether port 80 is available.

            *Test for Listening Ports*  
            `$ sudo netstat -lnp | grep :80`

            *Firewall rules*
            `$ sudo /sbin/iptables -L -n`

    - Troubleshoot Slow Networks 
        - DNS Issues 
            
            Ping, traceroute, route, netstat, and even iptables
        
        - Find the Network Slowdown with traceroute
            
            `$ traceroute yahoo.cn`
        
        - Find What Is Using Your Bandwidth with iftop
            iotop to identify what processes are consuming the most
            disk I/O. It turns out there is a tool called iftop that does something similar with network connections. Unlike top, iftop doesn’t concern itself with processes but instead lists the connections between your server and a remote IP that are consuming the most bandwidth. For instance, with iftop you can quickly see if your backup job is using up all your bandwidth
            by seeing the backup server IP address at the top of the output.
    
    - Packet Captures 
        - Use the tcpdump Tool      
                        
            It will scan through your network interfaces and choose the first suitable one; then it will capture, parse, and output information about the packets it sees. Here’s some example output from tcpdump with the -n option (so it doesn’t convert IP addresses to hostnames and slow things down) 
            
            `$ sudo tcpdump -n`

            >tcpdump: verbose output suppressed, use -v or -vv for full protocol decode listening on eth0, link-type EN10MB (Ethernet), capture size 96 bytes       
            19:01:51.133159 IP 208.115.111.75.60004 > 64.142.56.172.80: Flags [F.], seq 753858968, ack Ê1834304357, win 272, options [nop,nop,TS val 99314435 ecr 1766147273], length 0     
            19:01:51.133317 IP 64.142.56.172.80 > 208.115.111.75.60004: Flags 
            [F.], seq 1, ack 1, win Ê54, options [nop,nop,TS val 1766147276 ecr 99314435], length 0       
            19:01:51.157772 IP 208.115.111.75.60004 > 64.142.56.172.80: Flags [.], ack 2, win 272, options [nop,nop,TS val 99314437 ecr 1766147276], length 0
            19:01:51.224021 IP 72.240.13.35.45665 > 64.142.56.172.53: 59454% [1au] AAAA? ns2.example. Ênet. (45)
            19:01:51.224510 IP 64.142.56.172.53 > 72.240.13.35.45665: 59454*- 0/1/1 (90)
            19:01:51.256743 IP 201.52.186.78.63705 > 64.142.56.172.80: Flags [.], ack 1833085614, win Ê65340, length 0

            NOTE Whenever you are done capturing packets, just hit Ctrl-C to exit tcpdump. As tcpdump exits, it tells you how many packets it was able to capture and how many the kernel dropped.
            The output of tcpdump can be a bit tricky to parse at first, and I won’t go over all the columns, but let’s take two lines from the preceding output and break them down:

           > 19:01:51.224021 IP 72.240.13.35.45665 > 64.142.56.172.53: 59454% [1au] AAAA? ns2.example. Ênet. (45)       
           19:01:51.224510 IP 64.142.56.172.53 > 72.240.13.35.45665: 59454*- 0/1/1 (90)
           
            The first line tells you that at 19:01:51, the host 72.240.13.35 on port 45665 sent a packet to 64.142.56.172 on port 53 (DNS). If you wanted to dig further in that line you could see that the source host sent a request for the AAAA record (an IPv6 IP address)for ns2.example.net. The second line tells you that also at 19:01:51 the host 64.142.56.172 on port 53 replied back to host 72.240.13.35 on port 45665, presumably with an answer to the query.

            Since the first column is a datestamp for each packet, it makes it simple to see how long communication takes between hosts. This can be particularly useful for protocols that have set timeouts (like 30-second timeouts for DNS requests) since you can watch the timeout occur and see the source host resend its request. The next major column shows the IP and port for the source host. The > in the line can be treated like an arrow that lets you know that the direction of communication is from the first IP to the second. Finally, the next column tells you the destination IP and port followed by some extra flags, sequence numbers, and other TCP/IP information for that packet that we won’t get into here.
            Filtering Tcpdump Output Since by default tcpdump captures all of the packets it sees, it usually bombards you with a lot of noise that doesn’t help with your troubleshooting. What you want to do is pass tcpdump some filtering rules so it only shows you packets that you are interested in. For instance, if you were troubleshooting problems between your host and a server with a hostname of web1, you could tell tcpdump to only show packets to or from that host with 

            `$ sudo tcpdump -n host web1`
            
            If you wanted to do the opposite, that is, show all traffic except anything from web1, you would say
            
            `$ sudo tcpdump -n not host web1`

            You can also filter traffic to and from specific ports. For instance, if you wanted to just see DNS traffic (port 53) you would type 
            
            `$ sudo tcpdump -n port 53`

            If you wanted to capture all of your web traffic on either port 80 or port 443, you would type 
            
            `$ sudo tcpdump -n port 80 or port 443`

            You can actually get rather sophisticated with tcpdump filters, but it’s often easier to just capture a certain level of tcpdump output to a file and then use grep or other tools to filter it further. To save tcpdump output to a file, you can use a command-line redirect:
            
            `$ sudo tcpdump -n host web1 > outputfile`
            
            If you want to view the packets on the command line while they are being saved to a file, add the -l option to tcpdump so it buffers the output, and then use tee to both display the output and save it to a file:

            `$ sudo tcpdump -n -l host web1 | tee outputfile`
            
        - Raw Packet Dumps 
        
            Although you might think that tcpdump already provides plenty of difficult-to-parse output, sometimes all that output isn’t
            enough—you want to save complete raw packets. Raw packets are particularly useful since they contain absolutely all of the information about communication between hosts, and a number of tools (such as Wireshark, which we’ll discuss briefly momentarily) can take these raw packet dumps as input and display them in a much-easier-to-understand way. 
            The simplest way to save raw packet dumps is to run tcpdump with the -w option:

            `$ sudo tcpdump -w output.pcap`

            Like with other tcpdump commands, hit Ctrl-C to stop capturing packets.You can also use all of the same filtering options we’ve discussed so far when capturing raw packets. With raw packet dumps, you are getting the complete contents of the packets as best as tcpdump and your disk can keep up. So if someone is transferring a 1Gb file from your server, you might just capture the whole file in your packet dump. You may want to open up
            a second command-line session just so you can keep an eye on the size ofthe output file. tcpdump provides a few options you can use to manage the size of output files. The first option, -C, lets you specify the maximum size of the output file (in millions of bytes) before it moves on to a second one. So, for instance, if you wanted to rotate files after they grow past ten megabytes, you can type 
            
            `$ sudo tcpdump -C 10 -w output.pcap`
            
            The first output file will be named output.pcap.1, and once it gets to ten megabytes, tcpdump will close it and start writing to output.pcap.2, and so on, until you either kill tcpdump or you run out of disk space. If you want to be sure that you won’t run out of disk space, you can also add the -W option, which lets you limit the number of files tcpdump will ultimately create. Once tcpdump reaches the last file, it will start from the beginning and overwrite the first file in the set. So, for instance, if you want tcpdump to rotate to a new file after ten megabytes and want to make sure tcpdump only uses fifty megabytes of disk space, you could limit it to five rotated files:
            
            `$ sudo tcpdump -C 10 -W 5 -w output.pcap`

            Once you have these packet captures, you can use tcpdump to replay them as though they were happening in real time with the -r option. Just specify your raw packet output file as an argument. You can specify filters and other options like -n just as if you were running tcpdump against a live stream of traffic:

            `$ sudo tcpdump -n -r output.pcap`

            The tcpdump program is full of useful options and filters beyond what I’ve mentioned here. The man page (type man tcpdump) not only goes over all of these options and filters, but it also provides a nice primer on TCP packet construction, so it’s worth looking through if you want to dig deeper into tcpdump’s abilities.

        - Use Wireshark
---
### EDB
- Docker Questions
    - Diff between docker and VM.
    - Diff between containers and images.
    - How docker launch containers? Explain flow using component.
    - Function of REST API in docker.

- Python
    - What is Python Polymorphism?
    - What are differences between Py2 & Py3?
        - Python import
    - Multiple ways to write class in python?
    - Class methods and Function methods
    - Shallow vs Deep copy
    - Define function and class, create object of it.
    - Result of code 

     ```py
     l1 =[1,2,3]    
     l2 =[2,3,4]
     l2=[:]
     l1.append(l2) 
     print(l1,l2)
     ```
     - pytest write some tests for your program
     - functions of boto library.
- AWS
    - What are security groups?
        - Security groups act as a firewall for associated instances controlling both inbound and outbound traffic at the instance level.
    - What are regions and availability zones?
        - Amazon EC2 is hosted in multiple locations world-wide
        These locations are composed of regions and Availability Zones. Each region is a separate geographic area. Each region has multiple, isolated locations known as Availability Zones. Each region is completely independent. Each Availability Zone is isolated, but the Availability Zones in a region are connected through low-latency links. The following diagram illustrates the relationship between regions and Availability Zones.

    - How To Create Security Group In Amazon Ec2 ?
        - We can create Security Group in Amazon EC2 using the Amazon EC2 console. To launch instances in multiple regions, we’ll need to create a Security Group in each region.

        Following are the steps to create Security Group in Amazon EC2:

        >Open the Amazon EC2 console.   
        From the left navigation bar, select a region for the security group.   
        Click Security Groups in the navigation pane.   
        Click Create Security Group.    
        Enter a name for the new security group and a description.  
        In the VPC list, select your VPC.   
        On the Inbound tab, click Add Rule for each new rule, and then click Create.


---
### Vodafone
- [Ansible](https://gist.github.com/ramlaxman/84b2a3ad51288ecc77d0a9ed7a03001e)
    - What is ansible?
    - What are components of ansible?
    - What is Galaxy & Tower?
    - Write sample script for Ansible.
- AWS
    - How to connect your DB to AWS directly?
        - AWS Direct Connect to connect AWS with your internal network. One end of the cable is connected to your router the other to an AWS Direct Connect router. With this connection in place, you can create virtual interfaces directly to the AWS cloud.
    
    - What is VPC?
        - A virtual private cloud (VPC) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS cloud.You can launch your AWS resources, such as Amazon EC2 instances, into your VPC.You can configure your VPC; you can select its IP address range, create subnets, and configure route tables, network gateways, and security settings.

    - What is AWS Lambda function? How it is different than serverless?  
        - Serverless is an summarized idea of services being backed without    YOU managed servers. In the Amazon world serverless service           include: Lambda, DynamoDB, Machine Learning and various others.
        - Serverless is framework (serverless.com) used in AWS Lambda, Google Cloud function,Azure Functions & Kubeless for k8s to perform serverless tasks.
        - Sadly, "Serverless" is also the name of an open source framework that aides in writing code specifically for *compute* serverless architectures such as Lambda.
        - Lambda is a part of Serverless Stack [explained later] (the idea) and can be used with "Serverless" (the framework), though not a requirement. 
        - AWS Serverless Stack - A combination of AWS offered serverless technologies including API Gateway, Lambda, S3 and etc.
        > Case study of lambda
        - When Lambda was initially introduced it was challenging to develop Serverless applications using these technologies using Cloudformation. The problem was due to the complexity of writing Cloudformation for API Gateway and Lambda.

        - This is where Serverless Framework came in.

        -  Serverless Framework - An Open Source DevOps framework which simplifies defining API Gateway and Lambda using a simple file called serverless.yml. 
        
        - Since Serverless Framework uses conventions over configurations, it required only a few lines of code to define Lambda, API Gateway and etc. Underneath Serverless Framework generates Cloudformation based on whats defined in serverless.yml. In addition, Serverless Framework supported Multiple Cloud Providers.
        -  Later AWS introduced their own simplified scripting language called AWS SAM(Note: AWS SAM is not a Framework like Serverless with plugins and extension support as of now) to reduce the complexity in defining CloudFormation as an alternative to Serverless Framework.
        - AWS::Lambda::Function is the Cloudformation syntax to define a Lambda function.
        - AWS::Serverless::Function is the AWS SAM syntax to define a Lambda function which internally creates a Lambda function in Cloudformation (AWS::Lambda::Function) and related resources by convention when executing AWS SAM.
    - How will you create security groups in AWS?
    - How to create key pairs?

---
### Cybage
- AWS
    - What is purpose of lambda function: is it for application deployment or deploy over application? If yes, what have you among these?
        - Yes it is possible to deploy application using or on Lambda function
        as per Hands-on AWS guide.
        
        - It is also possible to deploy Lambda function in Application.
        
        - I have deployed code on AWS Lambda function.

        - *Deployments*:    
        This works amazingly well, where each deployment creates a new version of the Lambda. AWS allows to keep multiple versions of each Lambda and have aliases pointing to versions.

        - BaaS, i.e., Backend as a Service, is a Serverless backend (e.g., DB, hosting), i.e., a highly-available backend that can be set up with barely any configuration and can scale almost infinitely. Once created, the developer focuses on deploying code or data only.
        - FaaS, i.e., Function as a Service, is a Serverless product that hosts a piece of business logic (with a usually small footprint like resizing an image or sending an email). FaaS is very well suited to build Event-Driven architecture.

---
### Rebecca
- Python
    - How to iterate over items in dictionary?
        - `d.items()` makes it work.
    - List comprehension to print odd no in list
        - y = [x if x % 2 != 0 else '' for x in [1,2,3,4]]
    - What is polymorphism?
        - Use same function in different way within program is called polymorphism.
        ```py
        class Bear(object):
            def sound(self):
                print("Groarrr")
        
        class Dog(object):
            def sound(self):
                print("Woof woof!")
        
        def makeSound(animalType):
            animalType.sound()
            
        bearObj = Bear()
        dogObj = Dog()
        
        makeSound(bearObj)
        makeSound(dogObj)
        ```
--- 
### FireEye
- Python
    - Name 30 Lib in Python
        - General Purpose   
            - os
            - pip
            - setuptools
            - sys
            - http
            - copy
            - datetime
            - collections
            - math
            - itertools
            - pickle - python object serialization
            - csv
            - pipenv
            - maya
       - Internet Based
            - scrapy
            - requests
            - beautifulSoap
            - flask
            - django
            - bottle
            - django-restful
            - bottle-restful
            - flask-restful
        - Cloud Development:
            - Boto3
            - json
            - chalice
            - nameko
            - zappa
            - pyyaml
        - Database
            - redis-py
            - pymongo
        - ML:
            - keras
            - tensorflow
            - scikit-learn
            - numpy
            - pandas
            - scipy
    - Using REST API, fetch image as requested by user.
---
### Afour
- Python
    - What is shallow copy and deep copy?   
        ```py 
        import copy
        xs = [[1, 2, 3]]
        ys = list(xs) # or ys = copy.copy(xs)
        print(xs,ys)

        xs.append('new_obj')
        print(xs,ys)

        xs[0][1] = 'A'
        print(xs,ys)

        print('\n')

        # In deep copy, changes ONLY reflect in ORIGINAL
        xs = [[1, 2, 3]]
        ys = copy.deepcopy(xs)
        print(xs,ys)

        xs.append('new_obj')
        print(xs,ys)

        xs[0][1] = 'A'
        print(xs,ys)
        ```
    - How to print string in reverse order?

        *Method 1*:
        ```py
        sentence = 'how are you'
        first = sentence.split()       #  ['how','are','you'] in 'first'
        final = first[::-1]             #  ['you','are','how'] in 'final'
        ' '.join(final)                    
        'you are how'
        ```

        *Method 2*:
        one liner
        
    - What is use of serialization?
    - 
        
- Openstack
    - What are storage types?
        Block, Object, File, Tape.
---
### Accion Labs
- AWS
    - What is Serverless in AWS?
    - What are step functions?
    - Have you developed any API?
    - Explain steps in creation on Lambda function for Python App.

- Linux
    - How will you schedule jobs in Linux?

---
---
