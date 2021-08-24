## Prerequisites
1. Install Docker [10 mins]
    1. [Windows](https://www.youtube.com/watch?v=5nX8U8Fz5S0#t=01m00s)
    2. [Mac OSX](https://docs.docker.com/get-docker/)
    3. [Linux](https://docs.docker.com/get-docker/)

2. Getting familiar with terminal [10 mins]
    1. [Windows](https://www.computerhope.com/issues/chusedos.htm)
    2. [Mac OSX](https://medium.com/@grace.m.nolan/terminal-for-beginners-e492ba10902a)
    3. Linux - Do you really need me to help you??

3. Setup PSQL on docker [10 mins]
    1. Test if docker is working fine using - `docker version` on your terminal. You should see something like this. ![MarineGEO circle logo](/X1/res/docker-version-output.png) 
    This will show the basic details and version of your engine that you can use to debug things later on.
    2. Create a new directory call `database` anywhere on you system. You can either test the 
    3. Add a new file called `docker-compose.yml` and add the contents of the [following file]() into that.
    4. At this point your folder structure should look like this.
        ```txt
        database/
        ──── docker-compose.yml
        ```
    5. Open you terminal and [navigate to the directory](https://www.macworld.com/article/221277/command-line-navigating-files-folders-mac-terminal.html) that you created. You can check the currently directory using either the `pwd` or `cd ,`.
    6. Create your own instance of PSQL using this command `docker-compose up -d`. You should be able to see and output like this on your terminal. #TODO: Insert Image.
