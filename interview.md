#INTERVIEW QUESTIONS

```c
//MAX LENGTH SUB STRING WITHOUT DUPLICATES
#include<iostream>
#include<cstring>
#include<vector>
using namespace std;
string maxsubstr(string s)
{
        int start=0,max=0,maxstart=0;
        vector<int>lastid(256,-1);//last index of each character
        for(int i=0;i<s.size();i++)
        {
                char c=s[i];
                if(lastid[c]>=start)
                {
                        start=lastid[c]+1;//movestart prev occurence
                }
                lastid[c]=i;
                if(i-start+1>max)
                {
                        max=i-start+1;
                maxstart=start;
        }
}
return s.substr(maxstart,max);
}
int main()
{
        string s="abcdefabc";
        string r=maxsubstr(s);
        cout<<"substr="<<r<<"len:"<<r.size()<<endl;
}


//BACKGROUND SERVICE EXAMPLE PROGRAM
#include<iostream>
#include<unistd.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<syslog.h>
using namespace std;
void daemon()
{
        pid_t pid=fork();
        if(pid>0)exit(EXIT_SUCCESS);
        if(pid<0)exit(EXIT_FAILURE);
        if(setsid()<0)exit(EXIT_FAILURE);
        umask(0);
        chdir("/");
        close(STDIN_FILENO);
        close(STDOUT_FILENO);
        close(STDERR_FILENO);
        openlog("mydeamon",LOG_PID,LOG_DAEMON);
        syslog(LOG_NOTICE,"daemon started");
}
void dowork()
{
        syslog(LOG_INFO,"daemon heart");
}
int main()
{
        daemon();
        int interval=5;
        while(true)
        {
                dowork();
                sleep(interval);
        }
        closelog();
        return EXIT_SUCCESS;
}
commands:g++ -std=c++11 -o bacground bacground.cpp
tail -f /var/log/syslog

```
