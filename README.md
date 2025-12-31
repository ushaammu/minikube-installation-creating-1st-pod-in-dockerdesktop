# minikube-installation-creating-1st-pod-in-dockerdesktop
PS C:\Users\USHA CT>
PS C:\Users\USHA CT> kubectl version --client
Client Version: v1.34.1
Kustomize Version: v5.7.1
PS C:\Users\USHA CT> Move-Item $HOME\Downloads\minikube.exe $HOME\bin\
>>
Move-Item : Cannot find path 'C:\Users\USHA CT\Downloads\minikube.exe' because it      
does not exist.
At line:1 char:1
+ Move-Item $HOME\Downloads\minikube.exe $HOME\bin\
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\USHA CT\Downloads\minikube.ex  
   e:String) [Move-Item], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.MoveItemComm  
   and

PS C:\Users\USHA CT> dir $HOME\bin


    Directory: C:\Users\USHA CT\bin


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        31-12-2025     20:59       44580864 kubectl.exe
-a----        31-12-2025     21:08      140558336 minikube.exe


PS C:\Users\USHA CT> & "$HOME\bin\minikube.exe" delete --all
>>
* Deleting "minikube" in docker ...
* Removing C:\Users\USHA CT\.minikube\machines\minikube ...
* Removed all traces of the "minikube" cluster.
* Successfully deleted all profiles
PS C:\Users\USHA CT> docker pull gcr.io/k8s-minikube/kicbase:v0.0.48
>>
v0.0.48: Pulling from k8s-minikube/kicbase
Digest: sha256:7171c97a51623558720f8e5878e4f4637da093e2f2ed589997bedc6c1549b2b1
Status: Image is up to date for gcr.io/k8s-minikube/kicbase:v0.0.48
gcr.io/k8s-minikube/kicbase:v0.0.48
PS C:\Users\USHA CT> & "$HOME\bin\minikube.exe" start --driver=docker
>>
* minikube v1.37.0 on Microsoft Windows 11 Home Single Language 10.0.26200.7462 Build 26200.7462
* Using the docker driver based on user configuration
* Using Docker Desktop driver with root privileges
* Starting "minikube" primary control-plane node in "minikube" cluster
* Pulling base image v0.0.48 ...
* Creating docker container (CPUs=2, Memory=3072MB) ...  
! Failing to connect to https://registry.k8s.io/ from inside the minikube container    
* To pull new external images, you may need to configure a proxy: https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
* Preparing Kubernetes v1.34.0 on Docker 28.4.0 ...  
* Configuring bridge CNI (Container Networking Interface) ...
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Enabled addons: storage-provisioner, default-storageclass
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
PS C:\Users\USHA CT> & "$HOME\bin\minikube.exe" status
>>
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

PS C:\Users\USHA CT> & "$HOME\bin\minikube.exe" dashboard
>>
* Enabling dashboard ...
  - Using image docker.io/kubernetesui/dashboard:v2.7.0
  - Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
* Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server

* Verifying dashboard health ...
* Launching proxy ...
* Verifying proxy health ...
* Opening http://127.0.0.1:50892/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
PS C:\Users\USHA CT> kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:62020
CoreDNS is running at https://127.0.0.1:62020/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.       
PS C:\Users\USHA CT> kubectl get nodes
NAME       STATUS   ROLES           AGE    VERSION
minikube   Ready    control-plane   2m1s   v1.34.0
PS C:\Users\USHA CT> notepad pod.yaml
PS C:\Users\USHA CT> run kubectl apply -f pod.yaml
run : The term 'run' is not recognized as the name of a cmdlet, function, script 
file, or operable program. Check the spelling of the name, or if a path was included,  
verify that the path is correct and try again.
At line:1 char:1
+ run kubectl apply -f pod.yaml
+ ~~~
    + CategoryInfo          : ObjectNotFound: (run:String) [], CommandNotFoundExcepti  
   on
    + FullyQualifiedErrorId : CommandNotFoundException

PS C:\Users\USHA CT> kubectl apply -f pod.yaml    
pod/my-pod created
PS C:\Users\USHA CT> kubectl get pods
NAME     READY   STATUS              RESTARTS   AGE
my-pod   0/1     ContainerCreating   0          15s
PS C:\Users\USHA CT> kubectl describe pods
Name:             my-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Wed, 31 Dec 2025 22:22:57 +0530
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
  IP:  10.244.0.5
Containers:
  nginx-container:
    Container ID:   docker://0477996756e110de71d594b21300dd5d21b227d391a2feeff592a78d77420d9a
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:ca871a86d45a3ec6864dc45f014b11fe626145569ef0e74deaffc95a3b15b430
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 31 Dec 2025 22:23:22 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-jlqzf (ro)    
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-jlqzf:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s 
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  54s   default-scheduler  Successfully assigned default/my-pod to minikube
  Normal  Pulling    54s   kubelet            Pulling image "nginx"
  Normal  Pulled     30s   kubelet            Successfully pulled image "nginx" in 24.205s (24.205s including waiting). Image size: 151914258 bytes.
  Normal  Created    29s   kubelet            Created container: nginx-container       
  Normal  Started    29s   kubelet            Started container nginx-container        
PS C:\Users\USHA CT> kubectl create -f pod-without-port-label.yaml
error: the path "pod-without-port-label.yaml" does not exist
PS C:\Users\USHA CT> ^C
PS C:\Users\USHA CT> kubectl create -f "C:\Users\USHA CT\Downloads\pod-without-port-label.yaml"
>>
error: the path "C:\\Users\\USHA CT\\Downloads\\pod-without-port-label.yaml" does not exist
PS C:\Users\USHA CT> ^C
PS C:\Users\USHA CT> dir "C:\Users\USHA CT\Downloads"
>>


    Directory: C:\Users\USHA CT\Downloads


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----        22-04-2024     11:05                ApplicationForm_JA_org.aspx_files    
d-----        05-05-2025     15:26                arwshibernate
d-----        30-11-2024     20:55                background_images
d-----        10-06-2025     17:53                cake-shop-website-template
d-----        22-04-2025     16:54                cloud
d-----        30-11-2024     11:09                Datasets-main
d-----        12-10-2025     22:26                dcluttr
d-----        30-04-2025     07:44                eclipse-java-2025-03-R-win32-x86_64  
d-----        12-10-2025     23:59                Generate image output_files
d-----        18-12-2025     12:57                iperf-3.20-win64
d-----        18-12-2025     13:58                iperf3-windows-v0.3.4
d-----        16-10-2024     19:41                New Resume (2) _ Resume Editor_files 
d-----        02-03-2024     12:04                ONLINE_SHOPPING_SYSTEM_IN_PHP_WITH_S 
                                                  OURCE_CODE (1)
d-----        30-12-2023     16:53                OracleXE213_Win64
d-----        12-10-2025     23:46                output_files
d-----        29-11-2024     13:06                PowerBI-Datasets-main (1)
d-----        01-12-2025     12:49                router_files
d-----        07-05-2025     11:32                Sensors_interfacing
d-----        13-11-2025     14:28                terraform
d-----        13-11-2024     14:48                Terraform assignment
d-----        13-11-2025     14:20                terraform_1.13.5_windows_amd64       
d-----        06-02-2023     13:54                Turbo.C.3.2
d-----        16-04-2024     09:43                usha27_pybasic
d-----        25-06-2024     15:29                ushac
-a----        13-09-2024     19:53         433082 10th marks card.pdf
-a----        27-02-2025     15:35         374076 10th markscard.pdf
-a----        13-09-2024     19:53         440444 12th marks card.pdf
-a----        27-02-2025     15:35         364045 12th markscard.pdf
-a----        24-04-2025     22:58         973824 3 in 1 meter.ppt
-a----        07-05-2025     07:31         255065 3in1frontpage.pdf
-a----        19-03-2025     20:56         175378 3in1meter.pdf
-a----        24-04-2025     22:44        4788921 8thsem_projectwrk_report.pdf
-a----        27-02-2025     15:35        1152538 Aadhar_card.pdf
-a----        13-11-2025     12:22             87 add.py
-a----        01-08-2025     19:58         216757 adidasshoe.jpg
-a----        19-03-2025     21:15         292985 aicte_frontpage.docx
-a----        06-02-2025     14:34         182694 aicte_frontpage.pdf
-a----        11-10-2025     15:13      165609910 all_blinkit_category_scraping_stream 
                                                  .csv
-a----        26-11-2025     12:54        3049346 ammu.json
-a----        02-12-2025     09:03          77608 ammu.pkt
-a----        25-06-2024     15:56      948300296 Anaconda3-2024.02-1-Windows-x86_64.e 
                                                  xe
-a----        01-08-2025     19:07          82004 analysis of gold price
                                                  prediction.pptx
-a----        12-08-2025     11:48         328442 Analysis of Gold Price.ipynb
-a----        09-02-2025     19:01        1286384 aontestguide_cognizant.pdf
-a----        22-04-2024     11:05         143533 ApplicationForm_JA_org.aspx.html     
-a----        22-04-2025     15:46      157497056 arduino-ide_2.3.6_Windows_64bit.exe 
-a----        05-05-2025     15:25          11234 arwshibernate.zip
-a----        20-12-2025     13:17           4174 Assessment_Set_24.pdf
-a----        01-12-2025     22:13          41297 assignment.pkt
-a----        02-12-2025     15:18          37182 basic BGP.pkt
-a----        20-11-2024     20:34          73950 Big_Shop_Sales.xlsx
-a----        11-10-2025     15:18            139 blinkit_categories.csv
-a----        12-10-2025     23:36         385144 blinkit_cities_table.png
-a----        11-10-2025     15:18          16261 blinkit_city_map.csv
-a----        30-01-2025     17:07         759542 Blue and Gray Simple Professional    
                                                  CV Resume.pdf
-a----        22-04-2025     15:46         443886 Blynk-1.3.2.zip
-a----        10-06-2025     17:30         787138 cake-shop-website-template.zip       
-a----        27-05-2024     17:59         826490 chap5 softwaretesting.pdf
-a----        25-06-2024     14:40         283255 chat_app-main.zip
-a----        10-07-2024     05:57        8420232 ChromeSetup.exe
-a----        16-10-2024     15:02            125 citation-375960526.ris
-a----        19-05-2025     12:42         940210 cloudfront.pdf
-a----        27-05-2025     13:36        1108522 cloudibm.pdf
-a----        27-05-2025     13:35        2590808 cloudmain report.docx
-a----        19-05-2025     12:38        1106604 cloudmain report.pdf
-a----        31-07-2025     16:27         201477 cnn_imgdetection.pptx
-a----        25-10-2025     19:48       14681680 comet_installer_latest.exe
-a----        07-12-2025     18:17           9521 Copy of Karnataka_Enumeration_Form_T
                                                  racking_AC_Wise (13)(1).xlsx
-a----        20-11-2025     22:17         130252 crud1.jpg
-a----        20-11-2025     22:17         132771 crud2.jpg
-a----        20-11-2025     22:17         113306 crud3.jpg
-a----        20-11-2025     22:17         109152 crud4.jpg
-a----        20-11-2025     22:17         100279 crud5.jpg
-a----        30-11-2024     10:57       20652892 Datasets-main.zip
-a----        02-12-2024     16:04         374899 date.pbix
-a----        01-12-2025     12:57          40714 dec1.pkt
-a----        01-12-2025     23:14          41170 dec2.pkt
-a----        03-12-2025     16:40          41959 dec3.pkt
-a----        15-12-2025     15:11         754132 december15.pcapng
-a----        01-12-2025     22:12         107410 december1_hw.jpg
-a----        01-08-2025     22:00          88202 Deeplearning_imagedetection.ipynb    
-a----        28-11-2025     14:48          41491 DHCP for Multi-VLAN.pkt
-a----        01-08-2025     18:55         105194 diabetes_predictionml_project.pptx   
-a----        12-08-2025     11:46        2048389 diabetes_project.ipynb
-a----        28-11-2025     14:23          41188 DNS & DHCP pkt tracer.pkt
-a----        29-11-2025     10:09          74145 DNS server and website acess (1).pkt 
-a----        29-11-2025     10:53          74383 DNS server and website acess.pkt     
-a----        13-11-2025     09:35      588387760 Docker Desktop Installer.exe
-a----        13-11-2025     12:42            233 Dockerfile
-a----        04-03-2025     21:45          30927 DT20256732451_Application (1).pdf    
-a----        04-03-2025     21:36          29028 DT20256732451_Application.pdf        
-a----        13-11-2024     14:25        9054077 E-Commerce-Sales-Forecasting_.zip    
-a----        27-03-2025     13:21      164832608 eclipse-inst-jre-win64 (1).exe      
-a----        27-03-2025     13:23      359746328 eclipse-java-2025-03-R-win32-x86_64. 
                                                  zip
-a----        24-11-2024     19:45        5447071 EMS.pptx
-a----        20-12-2025     14:52        1916913 Evaluation_Dec20_set24.zip
-a----        18-11-2025     14:15             93 evenodd.py
-a----        17-05-2025     12:47        3144233 exactformat.docx
-a----        17-05-2025     12:47        1016034 exactformat.pdf
-a----        27-11-2024     19:49         544644 Final Project Proposal.docx
-a----        25-04-2025     00:25        2967314 FINARYR_REPORT.docx
-a----        01-12-2025     16:42          40927 floating routing.pkt
-a----        31-08-2024     13:00         300784 foodreport12[1].docx
-a----        02-11-2023     15:30        6498011 Front-end Developer Handbook.pdf     
-a----        20-04-2025     21:20         182139 front_pg_usha.docx
-a----        12-10-2025     23:59         514791 Generate image output.csv
-a----        03-11-2023     13:37       61263968 Git-2.42.0.2-64-bit.exe
-a----        18-07-2024     06:38         303744 gm usha.jpg
-a----        13-09-2024     19:53         460606 I'd proof .pdf
-a----        28-12-2024     20:05         110121 IBM PHASE 1 - USHA C T.pdf
-a----        13-09-2024     19:52         159140 id card.pdf
-a----        13-09-2024     19:56         123472 income_certificate.jpg
-a----        25-06-2024     14:25         177121 Intrenship Front Page.docx
-a----        20-02-2025     19:15       13459702 IOT_APPLICATION_MANAGEMENT.mp4      
-a----        18-12-2025     12:56        1181355 iperf-3.20-win64.zip
-a----        18-12-2025     13:09       10403095 iperf3-windows-v0.3.4.zip
-a----        01-08-2025     22:04          74557 irisflowerclassification.ipynb       
-a----        31-07-2025     16:25        1182274 IRISflowerclassification.pptx        
-a----        27-03-2025     13:21      215243888 jdk-23_windows-x64_bin (1).exe       
-a----        25-03-2025     15:59      215243888 jdk-23_windows-x64_bin.exe
-a----        16-10-2024     14:51         220962 join.aicte2.pdf
-a----        31-08-2024     11:28        1090709 Karnataka Village Accountant
                                                  RecruitmentExam Info.pdf
-a----        29-11-2025     10:52          40515 L3 switch configuration.pkt
-a----        13-12-2025     11:06         217696 lab5.pdf
-a----        16-12-2025     15:45           6483 linux-network-advanced-lab-steps.pdf 
-a----        16-12-2025     15:45          11219 Linux-Network-Lab.md
-a----        22-04-2025     15:46          20811 LiquidCrystal_I2C-1.1.2.zip
-a----        21-12-2023     14:16           5619 login.html
-a----        24-11-2025     17:22         125061 menu_output.jpg
-a----        31-12-2025     11:19       53713599 minikube-installer.exe
-a----        04-02-2025     16:03      239675560 MSB.exe
-a----        25-03-2025     15:21      369303552 mysql-installer-community-8.0.41.0.m 
                                                  si
-a----        20-11-2025     22:43          90247 name_age.jpg
-a----        03-12-2025     21:20          75689 NAT and PAT.pkt
-a----        08-12-2025     16:09      335303728 netgate-installer-amd64.iso.gz       
-a----        21-10-2025     02:22     1042892800 netgate-installer-v1.1-RELEASE-amd64 
                                                  .iso
-a----        16-10-2024     19:41        4124171 New Resume (2) _ Resume Editor.html  
-a----        25-09-2024     11:18       29601792 node-v22.9.0-x64.msi
-a----        27-11-2025     17:02          43343 nov27.pkt
-a----        31-07-2025     08:31      157291928 OBS-Studio-31.1.2-Windows-x64-Instal 
                                                  ler.exe
-a----        28-02-2024     14:34       16612106 ONLINE_SHOPPING_SYSTEM_IN_PHP_WITH_S 
                                                  OURCE_CODE (1).zip
-a----        28-02-2024     14:34       16612106 ONLINE_SHOPPING_SYSTEM_IN_PHP_WITH_S 
                                                  OURCE_CODE.zip
-a----        30-12-2023     16:49     1967615483 OracleXE213_Win64.zip
-a----        03-12-2025     22:36          41477 ospf quiz assessment.pkt
-a----        02-12-2025     14:01          45465 OSPF single and multi.pkt
-a----        12-10-2025     23:46         715910 output.html
-a----        01-12-2025     17:05          82107 own assignment.jpg
-a----        11-11-2025     13:59      154019600 PacketTracer-7.3.0-win64-setup.exe   
-a----        27-02-2025     15:43         543183 pancard.pdf
-a----        10-05-2025     10:29          18609 PatientData (1).xlsx
-a----        31-12-2024     10:14          87578 phase2_IBM_USHA.C.T.docx
-a----        31-12-2024     10:17         116862 phase2_IBM_USHA.C.T.pdf
-a----        27-11-2025     14:38          39770 pinging_packets.pkt
-a----        04-12-2025     12:14      149032576 Postman (x64).exe
-a----        29-11-2024     12:48       27245467 PowerBI-Datasets-main (1).zip        
-a----        20-04-2025     18:11        4850447 project report.pdf
-a----        22-05-2025     14:30         254553 project_frontpg.pdf
-a----        22-05-2025     14:30         181680 project_frontpg.pdf.docx
-a----        20-04-2025     20:47        4808098 project_report_final.pdf
-a----        01-12-2025     09:07        3831808 putty-64bit-0.83-installer.msi       
-a----        12-12-2025     14:15        1709672 putty.exe
-a----        22-06-2023     07:27      422872184 pycharm-community-2023.1.2.exe       
-a----        13-02-2025     15:51       28604208 python-3.13.2-amd64.exe
-a----        27-08-2024     16:33          73748 rama adharcard.jpg
-a----        23-12-2024     07:08         183714 Rescued document.pdf
-a----        25-11-2025     14:30          77666 resilient.jpg
-a----        02-12-2025     15:38          40542 RIP + OSPF.pkt
-a----        02-12-2025     15:04          40619 RIP assignment.pkt
-a----        02-12-2025     12:31          40697 RIPv2.pkt
-a----        01-08-2025     14:33         135362 Role-Based Student Management        
                                                  System in Django.pptx
-a----        01-12-2025     12:49         771023 router.html
-a----        20-11-2025     22:31          77439 runtop2.jpg
-a----        20-11-2025     22:31          82323 runtop3.jpg
-a----        20-11-2025     22:31          93903 run_top1.jpg
-a----        06-02-2025     10:51         441887 rural population.pdf
-a----        06-02-2025     11:22          20063 RURALCONTENT.docx
-a----        06-02-2025     11:22          29981 RURALCONTENT.pdf
-a----        09-02-2025     19:00         146729 sabtool_win8_10_11_v170530.zip       
-a----        27-08-2024     16:46          86953 salary slip.jpg
-a----        20-11-2024     20:36          44200 sample-data-10mins.xlsx
-a----        26-11-2025     10:05           1767 sample2 (1).json
-a----        26-11-2025     10:33        2700308 sample2.json
-a----        01-12-2025     14:18          46156 sampledec1.pkt
-a----        26-10-2023     08:57         218197 sarreeusha.jpg
-a----        19-11-2025     14:27            641 segregated_log.csv
-a----        13-09-2024     20:01          38966 selfdeclaration.jpg
-a----        18-03-2025     07:22         300379 seminar_topic2k25.pdf
-a----        27-05-2024     18:01         664989 software engg.pdf
-a----        29-11-2025     10:31          40595 spanning tree protocol.pkt
-a----        12-10-2025     23:56           2386 sqlquery.txt
-a----        29-11-2025     15:14          40777 standard_ACL.pkt
-a----        02-12-2025     17:27          41073 static routing with triangle
                                                  topology.pkt
-a----        01-12-2025     14:59          41206 static routing.pkt
-a----        17-11-2025     16:56           1328 stress-main.zip
-a----        10-05-2025     10:29           6213 student_records (1).xlsx
-a----        10-05-2025     10:29           5755 student_records_with_nan (1).xlsx   
-a----        16-10-2024     20:52         397635 SustainableWaterManagementinIndia.do 
                                                  cx
-a----        20-11-2025     22:52         101053 switch1.jpg
-a----        20-11-2025     22:52         124862 switch2.jpg
-a----        20-11-2025     22:52         119330 switch3.jpg
-a----        13-12-2025     11:12         190022 t1.jpg
-a----        13-12-2025     11:12         184824 t2.jpg
-a----        13-12-2025     11:12         211676 t3.jpg
-a----        13-12-2025     11:12         211676 t4.jpg
-a----        13-12-2025     11:12         182213 t5.jpg
-a----        13-12-2025     11:12          61222 t6.jpg
-a----        13-12-2025     11:12          70506 t7.jpg
-a----        09-12-2024     13:22      536136512 TableauPublicDesktop-64bit-2024-3-0. 
                                                  exe
-a----        13-12-2025     11:12         242778 task.jpg
-a----        13-12-2025     11:06         217696 task.py.pdf
-a----        02-12-2025     14:21          37282 task12.pkt
-a----        13-11-2024     14:57         406973 teraform asss (1).docx
-a----        13-11-2024     15:01         481958 teraform asss.docx
-a----        13-11-2024     14:55         728170 teraform asss.pdf
-a----        13-11-2025     14:35       30311934 terraform_1.13.5_windows_amd64       
                                                  (1).zip
-a----        13-11-2025     14:18       30311934 terraform_1.13.5_windows_amd64.zip   
-a----        27-08-2024     16:32          81500 thimmappa adharcard.jpg
-a----        25-04-2025     00:22        1026048 threeinonemeter.ppt
-a----        06-02-2025     11:57        1009437 TOURISM.pdf
-a----        21-07-2025     21:35              0 train
-a----        19-09-2024     16:27           4316 trophyimg.jpeg
-a----        06-02-2023     13:54        7298700 Turbo.C.3.2.zip
-a----        19-12-2025     14:24      400556032 turnkey-core-18.1-bookworm-amd64.iso 
-a----        03-02-2023     19:15          78322 u.jpg
-a----        06-02-2023     17:40         125123 u1.jpg
-a----        15-10-2024     14:27         184330 U1TRIAL.pdf
-a----        05-02-2025     16:56         118508 uam.jpg
-a----        13-11-2025     10:49     6345887744 ubuntu-24.04.3-desktop-amd64.iso     
-a----        27-08-2024     16:47         212245 usha 4th sem .pdf
-a----        27-08-2024     16:47         229618 usha 5th sem.pdf
-a----        27-08-2024     16:34          52344 usha adharcard.jpg
-a----        12-09-2024     20:59         166149 usha ammu.pdf
-a----        12-09-2024     21:04         166339 usha ammu1.pdf
-a----        05-02-2025     23:03        1130480 usha appropriate technologies.docx   
-a----        06-02-2025     11:36         720910 usha appropriate technologies.pdf    
-a----        31-08-2024     13:02         300784 usha food report.docx
-a----        27-08-2024     16:47          23566 usha passbook.jpg
-a----        20-02-2025     20:33         479599 usha phase4[1].pdf
-a----        12-09-2024     20:04         167255 usha resume final1.pdf
-a----        22-09-2024     18:32          59358 usha resume.docx
-a----        12-09-2024     20:30         165969 usha resume.pdf
-a----        12-09-2024     19:58         166154 usha resume1.pdf
-a----        05-02-2025     22:11        1885165 usha tourism.docx
-a----        06-07-2024     17:18           2057 Usha Usha - Resume - IT EMPLOYEE.txt 
-a----        06-07-2024     20:58           3358 Usha Usha - Resume - Summer
                                                  Internship.txt
-a----        13-11-2024     15:06         351039 USHA.C.T(CAN_33556213).pdf
-a----        28-12-2024     20:08         110121 USHA.C.T.pdf
-a----        13-12-2024     11:01         429297 usha.c.t.zip
-a----        25-03-2025     14:46         195994 usha.c.t_delltechnologies.pdf       
-a----        05-01-2025     13:46          23625 usha.c.t_ibm_phase3.docx
-a----        05-01-2025     13:48          39508 usha.c.t_ibm_phase3.pdf
-a----        09-02-2025     18:18         227599 USHA.C.T_IBM_PHASE4.pdf
-a----        26-02-2025     17:22         197386 usha.c.t_tcs.pdf
-a----        03-02-2023     16:34         153832 usha.jpg
-a----        12-12-2025     14:00           1422 usha.ppk
-a----        12-09-2024     21:09         166502 usha27.pdf
-a----        12-12-2025     14:18           1678 usha27.pem
-a----        12-12-2025     14:39           1426 usha@123.ppk
-a----        12-12-2025     14:34           1425 usha@27.ppk
-a----        02-12-2025     09:03          42223 ushaacl.pkt
-a----        10-02-2023     21:02         167285 ushaammu.jpg
-a----        10-02-2023     21:11         138426 ushachinni.jpg
-a----        19-05-2025     12:45         940228 ushacld.pdf
-a----        19-05-2025     10:48         940741 ushacloudint.pdf
-a----        15-10-2024     16:37          96727 ushacv_final.docx
-a----        15-10-2024     16:38         149861 ushacv_final.pdf
-a----        05-02-2025     23:18         838189 ushafood.pdf
-a----        05-02-2025     23:15         182778 ushafrontpg.pdf
-a----        27-05-2025     13:31         166024 ushaibm.pdf
-a----        03-02-2025     20:40         132266 ushapantech.csv
-a----        22-04-2024     11:07          39599 ushaphoto.jpg
-a----        26-10-2023     08:58          75490 ushaputti.jpg
-a----        12-09-2024     20:26         165776 ushaputti.pdf
-a----        22-09-2024     18:33         168058 ushaputti27.pdf
-a----        28-08-2024     18:29          66952 ushascholarship.pdf
-a----        22-04-2024     11:07          20439 ushasign.jpg
-a----        03-04-2023     14:13         168798 ushatop.jpg
-a----        05-02-2025     23:18        1403841 ushatourism.pdf
-a----        02-03-2025     16:07        1641655 usha_BE.pdf
-a----        30-05-2025     07:20         290043 usha_cloudinternship.pptx
-a----        30-01-2025     20:22         155957 usha_cognizant.pdf
-a----        12-10-2025     23:57         240136 Usha_CT.pdf
-a----        27-02-2025     16:27         491097 usha_enrollmentform.pdf
-a----        27-02-2025     15:35        2154086 usha_markscard.pdf
-a----        16-04-2025     22:43         455365 usha_palletechnologies.docx
-a----        20-02-2025     20:06         472069 usha_phase4.pdf
-a----        27-02-2025     15:47          67760 usha_photo - Copy.jpg
-a----        27-02-2025     15:47          67760 usha_photo.jpg
-a----        17-12-2023     15:50         115668 venkateshwaraimg.jpg
-a----        10-11-2025     16:22      176488552 VirtualBox-7.2.4-170995-Win.exe      
-a----        29-11-2025     10:53          43575 vln_assignment.pkt
-a----        15-12-2025     16:01         705260 vmwireshark.pcapng
-a----        13-02-2025     16:05      105610184 VSCodeUserSetup-x64-1.97.1.exe       
-a----        29-11-2025     10:53          40807 VTP lab configuration.pkt
-a----        21-10-2024     07:12          25952 water^0frontpg.pdf
-a----        16-10-2024     22:10         305856 water_aicte_report.pdf
-a----        16-10-2024     22:09         398191 water_aicte_report.pdf.docx
-a----        01-12-2025     12:42        1106976 WhatsApp Installer.exe
-a----        26-11-2025     10:44         919936 wifitest.json
-a----        10-12-2025     11:18        3826104 winrar-x64-713.exe
-a----        10-12-2025     12:15       25196296 winzip77-bing (1).exe
-a----        10-12-2025     11:19       25196296 winzip77-bing.exe
-a----        10-11-2025     14:29       95881032 Wireshark-4.6.0-x64.exe
-a----        15-12-2025     15:05         128664 wiresharkdec15.pcapng
-a----        02-03-2024     11:54      157583456 xampp-windows-x64-8.2.12-0-VS16-inst 
                                                  aller.exe


PS C:\Users\USHA CT> kubectl create -f "C:\Users\USHA CT\Downloads\pod-witout-port-label.yaml"
>> 
error: the path "C:\\Users\\USHA CT\\Downloads\\pod-witout-port-label.yaml" does not exist
PS C:\Users\USHA CT> kubectl get pods -o wide
NAME     READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
my-pod   1/1     Running   0          6m54s   10.244.0.5   minikube   <none>           
<none>
PS C:\Users\USHA CT>
