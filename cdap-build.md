# CDAP Framework Build
## CDAP Build
Recursively clone in order to get “cdap-ui” module.

```bash
git clone –-recursive https://github.com/cdapio/cdap
```
 Open `cdap` in IntelliJ
Make sure JAVA_HOME is set.

Checkout to latest release(TAG-6.8.1)-
```bash
git checkout release/6.8
```



Using maven(3.9.0) - 

```bash
mvn clean package -DskipTests
```    


## Build Sandbox Dist zip - 

```bash
MAVEN_OPTS="-Xmx2048m" mvn clean package \
    -pl cdap-standalone,cdap-app-templates/cdap-etl,cdap-app-templates/cdap-program-report \
    -am -amd -DskipTests -P templates,dist,release,unit-tests
```
## Running Standalone(Backend)
- Select Run > Edit Configurations...
- Add a new "Application" run configuration
- Set "Main class" to be ``io.cdap.cdap.StandaloneMain`` and "cp" to cdap-standlone
- Modify Option > Set "VM options" to ``-Xmx1024m`` (for in-memory Map/Reduce jobs)
- Click "OK"

NOTE: This only runs backend and not the UI, Backend runs on port `11015` and UI at port `11011`
<br><br>


You can check if backend is working using any microservice `curl` request-

```bash
curl localhost:11015/v3/namespaces/
```


## Run UI
After running standalone(backend), we can run UI separately-

navigate to `cdap-ui` and run-

```bash
yarn dev
```
If yarn is not installed, alternatively run-

```bash
npx yarn dev
```

Now Ui can be accessed on port `11011` using  `localhost:11011/`
 
