# **Cloud HW2 - Application to Cloud**  
### **Target**: Deploy your own application on Azure Cloud  
1. Using both Azure VM && Azure Container services
2. For each result, please display your Student No. on the web page  

> When using the Azure Container Instance, please
>  - Create and Explain how to adopt your docker image  
>     * Naming the image with your Student No.  
>  - Run a container instance to demo your application  

## **Part1 - Application on Azure VM**   

**Step1. Open a sandbox**   
> To save the credit of the student account, open a sandbox first , then we can work under the directory of **mslearn**.   

![](https://i.imgur.com/ET6rSLG.png)

**Step2. Generate a SSH key to connect with Azure virtual machine**  
> The sandbox is correspond to the host and the virtual machine we're going to used will be created on Azure. To connect with the VM from the host(sandbox) there're two ways, password and SSH key. In this practice, I choose SSH key to verify my identity. So, I create a pair of SSH key on my host(sandbox) by using command `ssh-keygen -t rsa -b 4096` and default options with the following questions.

![](https://i.imgur.com/FDtYTO0.png)

**Step3. Create a Azure virtual machine**  
> Create a linux VM on azure  

![](https://i.imgur.com/NM0JgZf.png)  
> Copy the SSH public key we just create on the host(sanbox) that will be used when we try to log in this VM from the host.  

![](https://i.imgur.com/BB4HFKg.png)  
> Check the information and start deploy the resouce if no mistakes.  

![](https://i.imgur.com/N3oaIZf.png)


**Step4. Use SSH key to connect VM from sandbox**  
> Back to the host, we use the command `ssh username@IP address` to log in out VM.  

![](https://i.imgur.com/y8WSG44.png)

**Step5. Pull the files `index.html` and `Dockerfile` from github to azure VM**  
> I had put the `index.html` in my GitHub, so now I just to pull the files from my GitHub to the VM.  

![](https://i.imgur.com/k0YLLSq.png)

**Step6. Install Apache on azure VM**  
> To run a web service, we need to install Apache on the VM.  

![](https://i.imgur.com/LXbyzhN.png)

**Step7. Put `index.html` under a specify directory**  
> With Apache2 installed, when we open the website, it will find the HTML file which will be run under the directory `/var/www/html` with the file name `index.html`. So, we need to put our own `index.html` under the specify directory to let Apache open.  

![](https://i.imgur.com/LVF4zMv.png)

**Step8. Add a new networking rule**  
> Web sevice often us port 80 as the default port, but originally the Network setting of the VM didn't have a rule for http (port 80) that my lead to the error when Apache trying to open the HTML file. So, we need to add the rule fot http manually  

![](https://i.imgur.com/84FFohD.png)

**Step9. Result**  
> Then when we enter the IP address of this VM which is the same as we log in, we can see our own `index.html` file opened successfully.  

![](https://i.imgur.com/C9oxEoA.png)

---

## **Part2 - Application on Azure Container**   

**Step1. Create a container register**  
> To use container on Azure, we need to create a new resource of **Container Register** first.  

![](https://i.imgur.com/VlmRZnu.png)

**Step2. Tag an new image reference by the source image**  
> Open the Vitual box that I used to create `Dockerfile` and `image` last week. Use the command `docker images` to check whether the source image (image with the StudentID:10627122) is still exist.   
>  
> Because we need to push this image into the azure container, we need to create a new image reference to this source image with the tag `<login-server>/reference image`, in this practice is `louischen.azurecr.io/10627122:latest` with my studentID 10627122.

![](https://i.imgur.com/iQDyQiQ.png)

**Step3. Log in Azure container and push the image**  
![](https://i.imgur.com/E0zWNiM.png)  
> After the image is well prepared, we log in the Azure container from the host by using command `docker login <login-server>`, here is `docker login louischen.azurecr.io`. 
>  
>  Then push the prepared image to the azure container by using the following command `docker push <image>`, here is `docker push louischen.azurecr.io/10627122:latest`.
![](https://i.imgur.com/SueMbVn.png)

**Step4. Check the reposity**  
> Check the reposity of azure container register to make sure whether we push the image successfully.  
> 
> Here we can see a repository with the name of my studenID: 10627122  

![](https://i.imgur.com/yiJrHR0.png)

**Step5. Create a container instance**
> After the image successfully pushed, we create a **Container Instance**.
![](https://i.imgur.com/DVEJIMq.png)

**Step6.** Open the website  
> Finally, open the URL with the IP address of the container instance, we can see the studentID successfully shown on the web page.  

![](https://i.imgur.com/WPHCD70.png)
