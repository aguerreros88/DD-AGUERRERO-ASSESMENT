# DD-AGUERRERO-ASSESMENT
TEST DATA DOG
Alcides Guerrero

Content:
1. Setup the enviroment and Install Datadog Agent.
2. Collect Metrics.
3. Visualize Data.
4. Monitor Data.
5. Collect APM Data.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Setup the enviroment and Install Datadog Agent

First, i have downloaded and installed Vagrant 2.2.19 and Virtual Box 6.1, in my Windows 10 computer.
I have created a new folder to allocate all the files for the VM.

vagrant init hashicorp/bionic64

[![Setup-the-enviroment-1-1.png](https://i.postimg.cc/MT5qnL3k/Setup-the-enviroment-1-1.png)](https://postimg.cc/ygDw5Lzn)

Once  the virtual enviroment was ready, i run the VM:

vagrant up

[![Setup-the-enviroment-1-2.png](https://i.postimg.cc/qq8JkRfL/Setup-the-enviroment-1-2.png)](https://postimg.cc/vxZFhGZg)


[![Setup-the-enviroment-1-3.png](https://i.postimg.cc/qqGPbCV9/Setup-the-enviroment-1-3.png)](https://postimg.cc/Mfv3XHGD)

After the VM run, i proceed tosing up my trial Account in the Data Dog Web to install the  Agent: 
Then I have installed the Datadog agent: 

DD_AGENT_MAJOR_VERSION=7 DD_API_KEY=xxxxxxxxxxxxxxxxxxxx DD_SITE="datadoghq.com" bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_script.sh)"

[![Setup-the-enviroment-1-4.png](https://i.postimg.cc/pLvZV1jY/Setup-the-enviroment-1-4.png)](https://postimg.cc/fJHXBCBJ)

[![Setup-the-enviroment-1-5.png](https://i.postimg.cc/WpkY2yzt/Setup-the-enviroment-1-5.png)](https://postimg.cc/yW7yjvFz)

2.Collect Metrics

After the instalation of the Datadog agent, i have added tags to the configuration file: datadog.yaml located in: /etc/datadog.agent/.

[![collect-metric-2-1.png](https://i.postimg.cc/Bv2tZsrM/collect-metric-2-1.png)](https://postimg.cc/mc2T8x2H)

Once the tags are added and the file have been saved, i restarted and check the status of the DD Agent.

sudo systemctl restart datadog-agent
sudo systemctl status datadog-agent

[![collect-metric-2-2.png](https://i.postimg.cc/T2sxsFSw/collect-metric-2-2.png)](https://postimg.cc/yW02gQ74)

After confirm everything is working good, i have check on Datadog platform:

[![collect-metric-2-3.png](https://i.postimg.cc/44Yyn6RY/collect-metric-2-3.png)](https://postimg.cc/z318cRBN)

After done with the tags, i  proceed to install and integrate mysql with datadog platform.

sudo apt-get install mysql-server

[![collect-metric-2-4.png](https://i.postimg.cc/Jzfcdr3q/collect-metric-2-4.png)](https://postimg.cc/v4vV4dNg)

Then i have check the status of the mysql server:

[![collect-metric-2-5.png](https://i.postimg.cc/x1Mb8KHv/collect-metric-2-5.png)](https://postimg.cc/sMf20GTx)

To avoid issues when the VM start up, i have set auto system start up for MySQL Server:

[![collect-metric-2-6.png](https://i.postimg.cc/C50wvqdg/collect-metric-2-6.png)](https://postimg.cc/wyWKM3hf)

Next, i have create a database user with appropriate permissions to collect metrics from the database.

mysql> CREATE USER 'datadog'@'%' IDENTIFIED WITH mysql_native_password by '<UNIQUEPASSWORD>';

[![collect-metric-2-7.png](https://i.postimg.cc/MHpFK6FB/collect-metric-2-7.png)](https://postimg.cc/5YD3sV19)
  
Next, i have prepared mysql server, giving privilegies to collect the metrics:
  
[![collect-metric-2-8.png](https://i.postimg.cc/y8420HJM/collect-metric-2-8.png)](https://postimg.cc/rKjhL7Nj)

once we have created the user, grant the acces to DB, we can see the integration showed up in the UI:

[![collect-metric-2-9.png](https://i.postimg.cc/DzyhbTH2/collect-metric-2-9.png)](https://postimg.cc/75cdppqc)
  
[![collect-metric-2-10.png](https://i.postimg.cc/5NdMSvTK/collect-metric-2-10.png)](https://postimg.cc/5j3GxHx8)
  
After, i used the agent commands to verify MySQL is integrated:
  
[![collect-metric-2-11.png](https://i.postimg.cc/tJ9N9B7m/collect-metric-2-11.png)](https://postimg.cc/FdnLZgyj)  
  
Create a custom Agent check that submits a metric named my_metric with a random value between 0 and 1000.

Navigate to /etc/datadog-agent/conf.d and create a file for the Agent check, and added the following into my_metric.yaml and save the file.
  
[![collect-metric-2-12.png](https://i.postimg.cc/3xG1C0M1/collect-metric-2-12.png)](https://postimg.cc/LJHjmX8g)
  
Then navigate to /etc/datadog-agent/checks.d and create a file called my_metric.py and add the following code into the file.

 [![collect-metric-2-13.png](https://i.postimg.cc/65kL367v/collect-metric-2-13.png)](https://postimg.cc/SJGz1hfS)
  
After creating the files and added the code, i run the command: sudo -u dd-agent -- datadog-agent check my_metric to verify my metric:
  
[![collect-metric-2-14.png](https://i.postimg.cc/Vk9MkqQx/collect-metric-2-14.png)](https://postimg.cc/NKMLNr0D)
  
Showing my_metric in the summary: 
  
[![collect-metric-2-15.png](https://i.postimg.cc/wvrRGFLm/collect-metric-2-15.png)](https://postimg.cc/YG1S46Xr)
  
By default the custom check will run at 15 second intervals. Update the my_check.yaml file so that it runs at 45 second intervals:
  
[![collect-metric-2-16.png](https://i.postimg.cc/CKP4wGbF/collect-metric-2-16.png)](https://postimg.cc/HJMM27SK)
  
[![collect-metric-2-17.png](https://i.postimg.cc/NFpsnjWP/collect-metric-2-17.png)](https://postimg.cc/2LLNbrj4)
  
---------------------------------------------------------------------------------------------------------------------------------------------

QUESTION: 
  
- Can you change the collection interval without modifying the Python check file you created?

  Yes, you can update the collection interval in my_metric.yaml file that i have created.
  
  
-----------------------------------------------------------------------------------------------------------------------------------------------

  3. Visualize Data.
  
  

  


 


  




