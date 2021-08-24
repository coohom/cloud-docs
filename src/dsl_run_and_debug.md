# DSL Local operation and debugging

<!-- toc -->

## Environment setup

### PYTHON

It is recommended to use python 3.6 version and use Anaconda to install (the document description is based on this premise)

----

### Environment configuration

#### Use Git + source project

1. clone project

   ```bash
   git clone git@gitlab.qunhequnhe.com:kloudsim/kloudsim-ecs-sdk.git
   ```

2. Dependent installation

   Under the above project path, execute

   ```bash
   pip install -r requirements.txt
   ```

3. PYTHONPATH designation

   1. Run from the command line [^win]

      ```bash
      echo $PYTHONPATH #View the configured path, which can be saved
      source envsetup.sh #Use the environment setup script provided in the project, and specify the path as the superior of ksecs, such as kloudsim-ecs-sdk, or use the export statement directly
      ```
      [^win]: Windows recommends using IDE directly; if you want to use the command line, first add the path to the *environment variable*

   2. IDE operation

      Import the upper layer of ksecs, namely the project kloudsim-ecs-sdk, no need to configure the path

#### Use pip install + package
```bash
pip install ksecs==version -i http://nexus.qunhequnhe.com/repository/pypi-qunhe/simple --trusted-host nexus.qunhequnhe.com
```
Optional version:
- 21.1.0
- 21.2.0
- 21.3.0

----

## Run

### Add main function

Two ways:

1. Add main function to custom DSL py file
```python
if __name__ =='__main__':
    from ksecs import apply
    apply(_is_dsl=True) # As long as it is directly debugged in DSL, _is_dsl is True. If you want to directly use the demo data in resources,
```
2. Open the main function comment directly in demoDSL.py


### Configure running parameters (take demoDSL.py as an example)

1. View parameter requirements

You can use the command line to check the requirements and descriptions of the incoming parameters
```bash
python ksecs/resources/demoDSL.py -h
```
Result display:
```bash
optional arguments:
  -h, --help show this help message and exit
  -t T Type of shader to call
              Options:
              0 --> ENTITY;
              1 --> PIXEL;
              2 --> STRUCTURE
  -i I Enter path of cc world data
  -d D Eneter path of DSL file
  -o O Eneter path of output folder
  -s S Enter scene task id
  -p P Enter path of rasterization result
```

2. Parameter description
	- Required parameter -t
	- Optional parameters:
		- If the other parameters are not added, the demo related in resources will be used as the incoming parameter by default
		- If you specify by yourself,-i/d/o is required,-p is required for pixelshader
	- Debugging can ignore the parameter -s

3. Operation mode
	- Use default test resources
		- Command Line
		```bash
		python ksecs/resources/demoDSL.py -t 0 # Take entity processor as an example
		```
		-IDE
			- Code
				Just add a ptype parameter corresponding to the value of -t, such as `apply(ptype=0, _is_dsl=True)`
			- IDE parameter configuration
				Take Pycharm as an example, add -t 0 to the `Parameters` of `Run/Debug Configuration`

	- Use specific task resources
		- Command Line
		```bash
		python ksecs/app.py -i path of ccworld.json -d path of DSL.py -o path of output folder -t 1 -p path of rasterizeOutput # Take pixel processor as an example
		```
		-IDE
		Take Pycharm as an example, add in the `Parameters` of `Run/Debug Configuration`
		```bash
		-i path of ccworld.json
		-d path of DSL.py
		-o path of output folder
		-t 1
		-p path of rasterizeOutput
		```
----
## Download

It is recommended to use test resources directly for debugging during the development process;
When there is a problem with a specific task, download the specific task resource and perform local debugging

### Test resources

#### method of obtaining:
ksecs/resources

#### How to use:
Use the default test resources for *** in the above running mode***

### Specific task resource download

#### method of obtaining:
Use the debug module under ksecs
1. Check the parameters required for operation

```bash
python ksecs/debug/debug.py -h
 
usage: debug.py [-h] [-t T] [-e E] [-s S] [-p P]
 
optional arguments:
  -h, --help show this help message and exit
  -t T Type of resources to download
              Options:
              0 --> only json.gz;
              1 --> json.gz and DSL file;
              2 --> json.gz, DSL file and rasterizeOutput
  -e E Eneter env for cc-manage
  -s S Enter scene task id
  -p P Enter local path for download resources
```
2. Parameter description
	- -p: Required, specify the local path where the resource is downloaded
	To
	- -s: required field, id of specific task
	To
	- -t: The choice of downloading resources, the complete works of downloadable resources are ccWorld.json.gz, rasterize.json.gz, task_config.json.gz
	To
		- 0: Only download the above json.gz resource and decompress json to -p
		- Based on 1:0, generate DSL.py used by the user according to task_config.json
		- On a 2:1 basis, download all rasterize results to rasterizeOutput according to rasterize.json
		To
		The default is 1 when it is not passed in
		To
		- -e Resource download is through the cc-mange interface
		To
			- prod_test
			- prod
			- sit

3. Operation mode
```bash
python ksecs/debug/debug.py -p ksecs/debug/ -s ZQYPIUMTCZ5YC325LQFH3KA8_0 -e prod_test -t 2
```
#### How to use
Use specific task resources for *** in the above operation mode***