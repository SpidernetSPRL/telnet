# telnet
A simple telnet-like operations through a web page

<b>Rationale</b>

I can remember a time where ones could access any server (for instance some cheap web server space you'd rent) with simple tools such as FTP and Telnet. This time is slowly getting over; With the advent of cPanel, Git, Docker and the likes, accessing a simple server to test a development or implement a quick fix is becoming an increasingly complex task, requiring specialised tools, RSA keys and so on.

At the "low" end, "managers" such as cPanel which are supposed to help even an end user to run a server (which is a sane ambition, I presume) usually miss one random crucial feature that makes them useless for the problem you want to solve. This "missing feature" vary from implementation to implementation. Something like "<i>you can upload a zip file... to discover there is no unzip</i>" or whatever. The thing is that by adding an interface layer between you and the server, they block the ability to fiddle to find a solution.

At the "high" end, tools such as Git and Docker are great for what they have been designed to address: teams of corporate workers sharing code that go over hundreds of thousands lines, cluster of cloud servers and so on, but let's be honnest, in my everyday life I am most often dealing with small projects that are a few thousands lines, that wouldn't make sense sharing and which are running on a simple webserver.

For those easy projects, the day to day use of sophisticated tools can be a hassle: you edit your code locally, commit it with Git, which is replicated to the Docker server, you test the modification realise it isn't working as expected and you're going around for a new cycle. Depending on how complex your infrastructure is (dev servers, production servers, docker needing to be reinstanciated with your new code,...), this easily can takes minutes and make interactive testing (for instance running a command to see the result) uneasy.

Comparatively, a telnet or an FTP client allows you to log to the server, change the file right away and test the result. It won't do versionning, nor help you migrate your code to another server or share it on social media, nor does it look very nice or be friendly to use for the novice but you can run a test cycle in something like 5 seconds, allowing to develop or fix a code almost interactively, try executing the program and get the error message right away and so on.

Another inconvenience is that those complex tools requires to be installed on the machine you use.

This more or less means you need <i>your</i> machine to fix your code. Should you find a machine with the adequate tools installed (which is unlikely unless you live in a community of software devs), you'd still need your keys which in case you don't have a cloud based keyring might be problematic. Let's face it: fixing a problem in a hurry from a random machine is difficult. Again, on large projects, this is desirable: security is more important than flexibility.

Anyhow, I am not advocating the use of "simple" tools such as FTP or Telnet over sophisticated ones. I am just concerned that this "simple" option is getting more and more unavailable.

What we need ? A simple way to perform simple tasks, for instance:

    - change a config file,
    - edit a script,
    - upload files,
    - list files in a folder to see if they have the proper rights,
    - make a bunch of .cgi script I just uploaded executable,
    - list the tasks locate the rogue one and kill it,
    - zip a folder,
    - start a command that doesn't work to see what's the error message,
    - compile a small c script,
    - tail a log file,
    - etc 
    
In a word the kind of simple operations you would do during an urgent fix, to hunt a bug or to test a modification. There isn't, say, a real need for bash scripting or whatever. Single commands fill most of the use cases.

And yes: if it still can help you compare versions or transfer a project from server to server... why not, but this isn't the main mission.

We want this to be as easy to operate as possible: both easy to install on any server (on which you may have very limitted access: say a mutualised webserver space) and easy to call on any client machine (on which you may as well have limitted access: a cybercafe machine, or a family computer at the place you currently are) we may feel confortable to use.

The use of the application shouldn't leave traces on the client machine (installed software, downloaded source,...), and certainly nothing that could be used to gain access to the server.

This means in both cases (server and client machines) that it may prove difficult (in term of allowed system rights and "pollution" of the client machine) to install custom software. Should you have those rights, it's of no use to have a "simple" solution requiring you a lengthy installation procedure.

Let's face it: a web based application is likely the best option, hence this project.

In many cases, you will want to access a distant server because you're on a web project, or use a mutualised server that likely already runs a web server.

The most likely port that won't be blocked on your client machine is the web http port 80, and chances are that there will be a web browser available.

So the idea is to create a single CGI script that implements all the needed functionalities. No associated config files, images, html or whatever, no different version according to the type of server (linux, windows,...): the ideal is to install the whole thing just by copying a single file on the server. We don't want the CGI to rely on anything such as database, session retention, or whatever: we want its installation to be as little problematic as possible.

On the client side, just nothing to do: the browser already exists and you just have to call the script you added on the server.
