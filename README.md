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

