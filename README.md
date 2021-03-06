# CISCO DNA Center automation POV
Using DNAC APIs we can automate business workflows and start building/integrating business applications into the network. this is an example using the template editor in DNAC we are able to automate the assignment of vlan throughout the network based on a business logic, in this example we organize couple of network ports into logical rooms regardless of the switch, and then we use the API to assign vlans to the rooms, the app would go and update the vlans on the respective ports using DNAC APIs.
The prototype is built using a python Flask server and CISCO UI toolkit and cisco NeXt UI toolkit, the GUI allows the user to group ports into rooms and then assign vlans to rooms
## Install:

#### Clone the repo :
```
$ git clone https://github.com/gve-sw/DNAC_usecase
```

#### Install dependencies :
```
$ pip install flask
$ pip install WTForms
```

## Setup:
#### DANC details :
You can deploy this prototype with one of our CISCO DevNet DNAC lab sandboxes available [here](https://devnetsandbox.cisco.com).
Fill in the details of your DNAC server in the [DNAC.py](./DNAC.py) file
```python
dnac_host = 'you ip address or host'
dnac_user = 'your user '
dnac_pass = 'your passowrd '
```

#### Run script [dnachelper.py](./dnachelper.py):
Run this file the first time before runing the server, this will create the template in DNAC and genrate the template id and device Ids
```
$ python3 dnachelper.py
```
 - take note of the template id
 - take note of the devices id 

After execution
```
$ python3 dnachelper.py
.
.
.
##### Success! Template id : 90a5164d-8011-4d2f-a205-b6d2219d7cb6
##### Devices list :
Hostname                      ##Ip Address          ##Id                                                                    
3504_WLC                      ##10.10.20.51         ##50c96308-84b5-43dc-ad68-cda146d80290
```

#### Update files for your environment:

Update the template id in the file [DNAC.py](./DNAC.py)

```python
template_v_id = 'your template id goes here'
```

Update the device ids in the [rooms.js](./rooms.js) file :

```json
  "ports": [
    {
      "switch_id": "6a49c827-9b28-490b-8df0-8b6c3b582d8a",
      "id": "0",
      "name": "0/0/12"
    },
```
Note: you can add ports from different switches based on your demo, make sure to update server.py with the ports/updated accordingly 

```python
port = SelectField('Port', choices=[('',''),('0', 'Port 0/0/12'),('1', 'Port 0/0/13'),('2', 'Port 0/0/14'),('3', 'Port 0/0/15'),('4', 'Port 0/0/16'),('5', 'Port 0/0/17	')], validators=[validators.required()])
```
## Usage:

Launch the server by issuing 
```
$ python server.py
```
In a web browser open :
http://127.0.0.1:5000/start

Use the GUI to assign ports into different rooms, and then assign vlan to room, then you can login to the switches to check if the vlan modification went through

![alt text][GUI]

[GUI]:./static/img/GUI.png "Logo Title Text 2"
