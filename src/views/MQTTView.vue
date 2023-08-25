<template>





  <div id="app">
    
  
    <div class="sidebar">
        <p>User ID: </p>
        <p>Token: </p>
        <br>
        <div class="sidebar-content">
  
          <p style="color:white;"><button><a href="#/">IoT Dashboard</a></button></p>
          <p style="color:white;"><button><a href="#/SubscribePackage">Subscription Package</a></button></p>

          <br>
  
        <p style="color:white;"><u>Supported Protocol</u></p>
        <p style="color:white;"><button><a href="#/MQTT">MQTT Mosquitto Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/IoTCore">AWS IoT Core Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/HTTPS">HTTPS API Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/GRPC">GRPC Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/WebSocket">Web Socket Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/Modbus">Modbus TCP Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/OPCUA">OPC UA Endpoint</a></button></p>
        <p style="color:white;"><button><a href="#/COAP">COAP Endpoint</a></button></p>
        <br>
        <br>
        <p style="color:white;"><u>Official SDK Package</u></p>
        <p style="color:white;"><button><a href="#/IoTCore">Robomatics IoT SDK</a></button></p>
        <p style="color:white;"><button><a href="#/IoTCore">Third Party API</a></button></p>
        <br>
        <br>
        <p style="color:white;"><u>Developer Support</u></p>
        <p style="color:white;"><button><a href="#/Documentation">Documentation</a></button></p>
          <!-- Sidebar content -->
          </div>
      </div>
  
      <div class="navbar">
          <a href="#" @click="selectedLevel = 'Level 5 ERP'">Level 5 ERP</a>
          <a href="#" @click="selectedLevel = 'Level 4 WMS'">Level 4 WMS</a>
          <a href="#" @click="selectedLevel = 'Level 4 MES'">Level 4 MES</a>
          <a href="#" @click="selectedLevel = 'Level 3 SCADA/ HMI'">Level 3 SCADA/ HMI</a>
          <a href="#" @click="selectedLevel = 'Level 2 PLC'">Level 2 PLC</a>
          <a href="#" @click="selectedLevel = 'Level 1 Sensor and Actuator'">Level 1 Sensor and Actuator</a>
  
        <div class="logout">
          <a href="#" @click="logout">Logout</a>
        </div>
  
        </div>
  
  
  
      <div class="main" style="margin-top:50px; color:white;">
        <h2>MQTT Protocol</h2>
        <br>
        <br>
        <img src="Mosquitto.png" style="width:250px;">
        <div style="text-align:left;">
              <p>Not Secure & No authenticated</p>
              <br>
              <p>Endpoint : </p>
              <p>Port Number : 1883</p>
        </div>
        <!-- -->
  
  
  
  
  
  
        <div>

    </div>
  
  
  
    <div>
      <!---->
      <div>
        <input v-model="newPLCName"  style="line-height: 28px;" placeholder="PLC name">
        <input v-model="newPLCToken" style=" margin-left:30px; line-height: 28px;" placeholder="PLC token">
        <button @click="addPLC" class="grass-green-add-button" style="margin-left:30px;">Add PLC</button>
      </div>
      <br>
      <!---->
      <table>

    <div v-for="item in jsonData" :key="item.id">
      <tr>
          <td>

              <div @click="toggleDropdown('both', item.id)" class="row">
                  <div style="margin-top:20px; margin-bottom:20px;">{{ item.name }}</div>
              </div>

          </td>
          <td>
              <div @click="toggleDropdown('both', item.id)" class="row">
                  <div style="margin-top:20px; margin-bottom:20px;">{{ item.token }}</div>
              </div>
          </td>
          <td width="20%"><button class="red-alert-button" style="margin-left:30px;">Delete PLC</button></td>
          <td width="20%"><button class="ocean-blue-edit-button"  style="margin-left: 30px;">Edit Token</button></td>
               
      </tr>
      
      <div v-if="item.showAnalogAndDigital" class="dropdown">
                  <!---->
                     
                  <!--Digital-->

                  <div @click="toggleDropdown('digital', item.id)" class="row" style="border: 2px solid black; background-color: #2B65EC;">
                      <div style="margin-top:20px; margin-bottom:20px; ">Digital</div>

                
                  </div>

       
                      <div v-if="item.showDigitalDropdown" class="dropdown">


                              <div  >
                                  <!---<div style="margin-top:20px; margin-bottom:20px;">Digital: {{ item.digital }}</div>-->
                                  <!--For Loop PLC Digital Address / Channel-->
                                  <table>
                                    <tr>
                                        <h3><u>Channel</u></h3>
                                      </tr>

                                      <tr>
                                        <th>Address ID</th>
                                        <th>Address Name</th>
                                        <th>Address Description</th>
                                        <th>Delete</th>
                                        <th>Edit</th>

                                      </tr>
                                   
                                        <tr v-for="(address, addressIndex) in item.addresses" :key="addressIndex" style="text-align:left;">

                                                <td  @click="handleAddressClick(item.id, address.id)" style="margin-top:20px; margin-bottom:20px; cursor: pointer;" >{{ address.id }}  </td>
                                                <td  @click="handleAddressClick(item.id, address.id)" >{{ address.name }}  </td>
                                                <td v-if="!address.editing"   @click="handleAddressClick(item.id, address.id)">  {{ address.description }}</td>
                                                <td><button @click="showDeleteConfirmation(plcIndex, addressIndex)" class="red-alert-button">Delete</button></td>
                                                <td><button v-if="!address.editing" @click="editAddress(address)" class="ocean-blue-edit-button">&nbsp&nbspEdit Description&nbsp&nbsp</button></td>
                                               <!---
                                                <td>
                                                  <div class="lamp-container">
                                                      <div class="lamp">
                                                        <div class="bit on"></div>
                                                        <div class="bit off"></div>
                                                      </div>
                                                    </div>
                                                </td>
                                                --->

                                        </tr>
                                  </table>
                                  <!--End For Loop-->

                            <div v-if="item.showBitAddress" class="dropdown" style=" margin-left:50px;">
                                    <h3 style="text-align: left;"><u>Bit Address</u></h3>
                                  <table style="width:100%; text-align:left;">
                                    <tr>
                                      <th>Bit Address</th>
                                      <th>Bit Description</th>
                                      <th>Edit Description</th>
                                      <th>Bit Lamp</th>
                                    </tr>

                                      <tr v-for="item in bitAddress" :key="item.id" class="row" @click="toggleDropdown('both', item.id)">
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.bitAddress }}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.description }}</td>
                                      <td><button  @click="editAddress(address)" class="ocean-blue-edit-button">&nbsp&nbspEdit Description&nbsp&nbsp</button></td>
                                      <td>

                                        <div class="lamp-container">
                                                      <div class="lamp">
                                                        <div class="bit on"></div>
                                                        <div class="bit off"></div>
                                                      </div>
                                        </div>


                                      </td>

                                      </tr>

                                  </table>
                              </div>

                              </div>


                              <!---->
                              <div v-if="item.showAnalogDropdown" class="dropdown" style="border: 2px solid black;">
                                  <div style="margin-top:20px; margin-bottom:20px;"> Analog: {{ item.analog }}</div>
                              </div>


                  </div>
                  <!---->
                  <!---->
                     
                  <!--Analog-->

                          <div @click="toggleDropdown('analog', item.id)" class="row" style="border: 2px solid black; background-color: #7CFC00; color:black;">
                              <div style="margin-top:20px; margin-bottom:20px;">Analog</div>
                          </div>

                          <div v-if="item.showAnalogDropdown" class="dropdown" style="border: 2px solid black;">
                            <!----> 
                            
                            <table style="width:100%; text-align:left;">
                              <!--  {id:1 , AnalogAddress: 201, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},-->
                                    <tr>
                                      <th>Analog Address</th>
                                      <th>Analog Description</th>
                                      <th>Hexadecimal Value</th>
                                      <th>Decimal Value</th>
                                      <th>Maximum</th>
                                      <th>Minimal</th>
                                      <th>Edit</th>
                                      <th>Show Graph</th>

                                    </tr>

                                      <tr v-for="item in Analog_address" :key="item.id" class="row" @click="toggleDropdown('both', item.id)">
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.AnalogAddress}}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.description }}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.hexaValue }}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.DecimalValue }}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.Maximum }}</td>
                                      <td  style="margin-top:20px; margin-bottom:20px;">{{ item.Min }}</td>
                                      <td><button  @click="editAddress(address)" class="ocean-blue-edit-button">&nbsp&nbspEdit Description&nbsp&nbsp</button></td>
                                      <td></td>

                                      </tr>
                                      
                                  </table>

                            <!---->
                            
                          </div>
   
      </div>


    </div>

  </table>
  <!-- -->
  </div>
  
  
  

  
  

  
        
    
      </div>
    </div>
  
  
  
  </template>

<script>
export default {
 data() {
   return {
     bitAddress: [
         {id:1 , bitAddress: 100.01, description:"Alarm"},
         {id:2 , bitAddress: 100.02, description:"Alarm"},
         {id:3 , bitAddress: 100.03, description:"Alarm"},
         {id:4 , bitAddress: 100.04, description:"Alarm"},
         {id:5 , bitAddress: 100.05, description:"Alarm"},
         {id:6 , bitAddress: 100.06, description:"Alarm"},
         {id:7 , bitAddress: 100.07, description:"Alarm"},
         {id:8 , bitAddress: 100.08, description:"Alarm"},
         {id:9 , bitAddress: 100.09, description:"Alarm"},
         {id:10 , bitAddress: 100.10, description:"Alarm"},
         {id:11 , bitAddress: 100.11, description:"Alarm"},
         {id:12 , bitAddress: 100.12, description:"Alarm"},
         {id:13 , bitAddress: 100.13, description:"Alarm"},
         {id:14 , bitAddress: 100.14, description:"Alarm"},
         {id:15 , bitAddress: 100.15, description:"Alarm"},


     ],
     Analog_address: [
         {id:1 , AnalogAddress: 200, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:2 , AnalogAddress: 201, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:3 , AnalogAddress: 202, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:4 , AnalogAddress: 203, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:5 , AnalogAddress: 204, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:6 , AnalogAddress: 205, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:7 , AnalogAddress: 206, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:8 , AnalogAddress: 207, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:9 , AnalogAddress: 208, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:10 , AnalogAddress: 209, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:11 , AnalogAddress: 210, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:12 , AnalogAddress: 211, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:13 , AnalogAddress: 212, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:14 , AnalogAddress: 213, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:15 , AnalogAddress: 214, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:16 , AnalogAddress: 215, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:17 , AnalogAddress: 216, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:18 , AnalogAddress: 217, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:19 , AnalogAddress: 218, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:20 , AnalogAddress: 219, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:21 , AnalogAddress: 220, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:22 , AnalogAddress: 221, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:23 , AnalogAddress: 222, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:24 , AnalogAddress: 223, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:25 , AnalogAddress: 224, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:26 , AnalogAddress: 225, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:27 , AnalogAddress: 226, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:28 , AnalogAddress: 227, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:29 , AnalogAddress: 228, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:30 , AnalogAddress: 229, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:31 , AnalogAddress: 230, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:32 , AnalogAddress: 231, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:33 , AnalogAddress: 232, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:34 , AnalogAddress: 233, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:35 , AnalogAddress: 234, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:36 , AnalogAddress: 235, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:37 , AnalogAddress: 236, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:38 , AnalogAddress: 237, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:39 , AnalogAddress: 238, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},
         {id:40 , AnalogAddress: 239, description:"Temperature",hexaValue: "FFFF", DecimalValue:"65,535",Maximum:"3000","Min":"500"},


     ],
     jsonData: [
       {  id: 1, 
          name: 'PLC 1', 
          token: 'TOKEN123' ,
          analog: 'Analog 1', 
          digital: '100', 
          showAnalogDropdown: false, 
          showDigitalDropdown: false, 
          showAnalogAndDigital: false, 
          showBitAddress: false,
          addresses: [
            {id:100, name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
            { id:101, name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:102, name: '102', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:103, name: '103', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:104, name: '104', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:105, name: '105', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:106, name: '106', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:107, name: '107', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:108, name: '108', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:109, name: '109', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:110, name: '110', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:111, name: '111', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:112, name: '112', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:113, name: '113', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:114, name: '114', description: 'Description for Address 2 in PLC 4', editing: false },
            { id:115, name: '115', description: 'Description for Address 2 in PLC 4', editing: false },

            // Add more addresses with descriptions here
          ], 
      },
       {   id: 2, 
          name: 'PLC 2',
          token: 'TOKEN124' ,
          analog: 'Analog 2',
          digital: '101',
          showAnalogDropdown: false, 
          showDigitalDropdown: false,
          showAnalogAndDigital: false, 
          showBitAddress: false,
          addresses: [
              {id:100, name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              {id:101, name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
            // Add more addresses with descriptions here
          ], 
      },
       { id: 3, 
         name: 'PLC 3', 
         token: 'TOKEN125' ,
         analog: 'Analog 3',
        digital: '102',
        showAnalogDropdown: false, 
        showDigitalDropdown: false,
         showAnalogAndDigital: false, 
         showBitAddress: false,
         addresses: [
              {id:100, name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              {id:101, name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
            // Add more addresses with descriptions here
          ], 
      },

       // Add more items as needed
     ],
   };
 },
 methods: {
   toggleDropdown(type, id) {
     const index = this.jsonData.findIndex(item => item.id === id);
     if (index !== -1) {
       if (type === 'both') {
         this.jsonData[index].showAnalogAndDigital = !this.jsonData[index].showAnalogAndDigital;
         this.jsonData[index].showAnalogDropdown = false;
         this.jsonData[index].showDigitalDropdown = false;
       } else if (type === 'analog') {
         this.jsonData[index].showAnalogDropdown = !this.jsonData[index].showAnalogDropdown;
         this.jsonData[index].showDigitalDropdown = false;
       } else if (type === 'digital') {
         this.jsonData[index].showDigitalDropdown = !this.jsonData[index].showDigitalDropdown;
         this.jsonData[index].showAnalogDropdown = false;
       } else if (type === 'bitaddress') {
          alert(id);
         this.jsonData[index].showBitAddress = !this.jsonData[index].showBitAddress;
       }
     }
   },
   handleAddressClick(itemid, addressId) {
    // Do something with the clicked addressId
    console.log("Clicked address ID:", addressId);
    alert("Item ID: " + itemid +  " Address ID"+ addressId);
    // Call your toggleDropdown function here if needed
    // toggleDropdown('bitaddress', addressId);
    const index = this.jsonData.findIndex(item => item.id === itemid);
    this.jsonData[index].showBitAddress = !this.jsonData[index].showBitAddress;

  },
 },
};
</script>
  
  <style>
    .modal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 9999; /* Set the z-index to place the modal on top */
    }
  
    .modal-content {
      background-color: #fde2e8; /* Set the background color to white-pink */
      border: 2px solid #ff1493; /* Add a 2px border with pink color */
      padding: 20px;
      border-radius: 5px;
      color:black;
    }
  
  
    .modal-content button {
      /* Add styles for the "Close" button */
      border: 1px solid #000; /* Black border */
      padding: 8px 12px; /* Adjust padding as needed */
      background-color: #fff; /* White background */
      color: #000; /* Black text color */
      cursor: pointer;
      border-radius: 5px;
    }
  
    .modal-content button:hover {
      background-color: #000; /* Change background color on hover */
      color: #fff; /* Change text color on hover */
    }
  
  /* Styling for the black alert button */
  .dark-cancel-button {
    padding: 10px 20px;
    background-color: black; /* Change the background color to black */
    color: white;
    border: 2px solid darkgray; /* Change the border color to a darker shade of gray */
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  /* On hover effect */
  .dark-cancel-button:hover {
    background-color: darkgray; /* Change the hover background color to a darker shade of gray */
  }
  
  /* On click effect */
  .dark-cancel-button:active {
    background-color: dimgray; /* Use a darker shade of gray on click */
  }
  
  
  
  /* Styling for the purple alert button */
  .purple-save-button {
    padding: 10px 20px;
    background-color: purple; /* Change the background color to purple */
    color: white;
    border: 2px solid darkpurple; /* Change the border color to a darker shade of purple */
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  /* On hover effect */
  .purple-save-button:hover {
    background-color: darkpurple; /* Change the hover background color to a darker shade of purple */
  }
  
  /* On click effect */
  .purple-save-button:active {
    background-color: #800080; /* Use a darker shade of purple on click (here using hex code) */
  }
  
  
  
  
  /* Styling for the grass green alert button */
  .grass-green-add-button {
    padding: 10px 20px;
    background-color: #3CB371; /* Use your preferred grass green color code */
    color: white;
    border: 2px solid #2E8B57; /* Use a slightly darker shade of grass green for the border */
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  /* On hover effect */
  .grass-green-add-button:hover {
    background-color: #2E8B57; /* Use a slightly darker shade of grass green on hover */
  }
  
  /* On click effect */
  .grass-green-add-button:active {
    background-color: #228B22; /* Use a darker shade of grass green on click */
  }
  
  
  /* Styling for the ocean blue alert button */
  .ocean-blue-edit-button {
    padding: 10px 20px;
    background-color: #007BAC; /* Use your preferred ocean blue color code */
    color: white;
    border: 2px solid #005A80; /* Use a slightly darker shade of ocean blue for the border */
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  /* On hover effect */
  .ocean-blue-edit-button:hover {
    background-color: #005A80; /* Use a slightly darker shade of ocean blue on hover */
  }
  
  /* On click effect */
  .ocean-blue-edit-button:active {
    background-color: #00416A; /* Use a darker shade of ocean blue on click */
  }
  
  /* Styling for the red alert button */
  .red-alert-button {
    padding: 10px 20px;
    background-color: red;
    color: white;
    border: 2px solid darkred;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
  }
  
  /* On hover effect */
  .red-alert-button:hover {
    background-color: darkred;
  }
  
  /* On click effect */
  .red-alert-button:active {
    background-color: crimson;
  }
  
  
  
  .sidebar {
    width: 200px;
    position: fixed; /* Position the sidebar as fixed */
    top: 0;
    bottom: 0; /* Extend the sidebar to the bottom */
    left: 0;
    overflow-y: auto; /* Enable vertical scrolling if content overflows */
    background-color: #111;
    padding-top: 20px;
    padding-bottom: 20px; /* Add padding at the bottom of the sidebar */
    color: white; /* Set text color */
    
  }
  
  .sidebar-content {
    /* Adjust padding as needed */
    padding: 20px;
  }
  
  .sidebar a {
    display: block;
    color: white;
    padding: 16px;
    text-decoration: none;
  }
  
  .sidebar a:hover {
    background-color: #ddd;
    color: black;
  }
  
  /* Main content styles */
  .main {
    margin-left: 200px; /* Same as the width of the sidebar */
    padding: 20px;
  }
  
  table {
    border-collapse: collapse;
    width: 100%;
  }
  
  th, td {
    border: 1px solid black;
    padding: 8px;
    text-align: left;
  }
  
  
  /* Navbar styles */
  .navbar {
    background-color: #333;
    overflow: hidden;
    width: 100%;
    position: fixed; /* Position the navbar as fixed */
    top: 0; /* Place the navbar at the top */
    left: 200px; /* Align with the sidebar */
    z-index: 2; /* Add z-index to position the navbar above the main content */
  }
  
  .navbar a {
    float: left;
    display: block;
    color: white;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
  }
  
  .navbar a:hover {
    background-color: #ddd;
    color: black;
  }
  
  /* Right-aligned logout button */
  .logout {
    display: flex;
    align-items: center;
  }
  
  .logout a {
    color: white;
    padding: 14px 16px;
    text-decoration: none;
  }
  
  .logout a:hover {
    background-color: #ddd;
    color: black;
  }
  
  
  
  /* Style for the dropdown buttons */
  .dropdown-button {
    margin-top: 10px; /* Add margin to the top */
    margin-bottom: 10px; /* Add margin to the bottom */
    padding: 5px 10px; /* Adjust padding as needed */
    color: black; /* Black text color */
    cursor: pointer;
    border-radius: 5px;
    text-align: center; /* Center-align the button content */
  
  }
  
  .dropdown-option {
    display: block;
    width: 100%;
    padding: 10px;
    border: none;
    text-align: left;
    cursor: pointer;
  }
  /* Bit Lamp*/
    /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/

  .lamp-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.lamp {
  display: flex;
}

.bit {
  width: 20px;
  height: 20px;
  margin: 2px;
  border-radius: 50%;
}

.on {
  background-color: green;
}

.off {
  background-color: gray;
}
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/
  /* Bit Lamp*/

  </style>