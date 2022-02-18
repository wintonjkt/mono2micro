# Mono2Micro by Example


1. Clone the sample app git repo
```
git clone https://github.com/nheidloff/application-modernization-javaee-quarkus.git && cd application-modernization-javaee-quarkus 
ROOT_FOLDER=$(pwd)
```
2. Download mono2micro from https://epwt-www.mybluemix.net/software/support/trial/cst/programwebsite.wss?siteId=911&h=null&p=null 
   Files to download:  
  * https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/mono2micro/Mono2Micro-Monolith-DataCollector.zip  
  * https://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/mono2micro/Mono2Micro-Example.zip  
  * Put the files in ${ROOT_FOLDER}/mono2micro/tool and Unzip the files  
3. Pull the mono2micro docker files
```
docker pull ibmcom/mono2micro-bluejay	
docker pull ibmcom/mono2micro-aipl	
docker pull ibmcom/mono2micro-ui	
docker pull ibmcom/mono2micro-cardinal
```
4. Modify the application source code to contain debug information when which classes and methods are invoked.
```
docker run -e LICENSE=accept --rm -it -v ${ROOT_FOLDER}/:/var/application ibmcom/mono2micro-bluejay /var/application/monolith-open-liberty
cp ${ROOT_FOLDER}/monolith-open-liberty-klu/refTable.json ${ROOT_FOLDER}/mono2micro/output/tables
cp ${ROOT_FOLDER}/monolith-open-liberty-klu/symTable.json ${ROOT_FOLDER}/mono2micro/output/tables
```
5. launch your application with the modified source code.  
```
sh ${ROOT_FOLDER}/scripts-docker/build-and-run-monolith-db2.sh
sh ${ROOT_FOLDER}/scripts-docker/build-and-run-splitted-frontend-open-klu.sh
```
  
Reference:  
http://heidloff.net/article/step-by-step-instructions-mono2micro/

### Docker Compose Troubleshoot  

ImportError: cannot import name IPAMConfig  
```
pip uninstall docker
pip uninstall docker-py
pip uninstall docker-compose
pip install docker-compose==1.9.0
```
