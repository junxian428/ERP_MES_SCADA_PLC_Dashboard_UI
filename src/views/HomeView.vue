<template>





<div id="app">
  

  <div class="sidebar">
      <p>User ID: {{ userID }}</p>
      <p>Token: {{ userToken }}</p>
    
      <div class="sidebar-content">

        <div class="dropdown" style="color:black;">
          <button><a href="#/">        <img src="FACTORY.png" style="width:100px;">SCADA Dashboard</a></button>
          <div class="dropdown-content">
            <a href="#" style="color:black;">Customize your own dashboard</a>
            <a href="#" style="color:black;">Settings</a>
          </div>
        </div>
  
  <p style="color:white;"><button><a href="#/loghistorian"><img src="LOG.png" style="width:100px;">Log Historian</a></button></p>
        <p style="color:white;"><button><a href="#/SubscribePackage">  <img src="DEAL.png" style="width:100px;">Subscription Package</a></button></p>
        <br>
        <hr>
        <br>
        <h3 style="color:white;">Messaging API Setup</h3>
        <p style="color:white;"><button><a href="#/Telegram"> <img src="TELEGRAM.png" style="width:100px;">Telegram Setup</a></button></p>
        <p style="color:white;"><button><a href="#/"><img src="WHATSAPP.png" style="width:100px;">WhatsApp Setup</a></button></p>
        <br>
        <hr>
        <br>
        <h3 style="color:white;">Maintainence Team Performance System</h3>
        <p style="color:white;"><button><a href="#/MaintainenceTeamTracker"><img src="MAINTAIN.png" style="width:100px;">Maintainence Team Tracker</a></button></p>
        <p style="color:white;"><button><a href="#/MaintainenceTeamTracker"><img src="REPORT.jpg" style="width:100px;">Maintainence Team Report</a></button></p>
        <br>
        <hr>
        <br>

      <h3 style="color:white;">Supported Protocol</h3>
      <p style="color:white;"><button><a href="#/MQTT"><img src="MOSQUITTO_LOGO.png" style="width:100px;">MQTT Mosquitto Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/IoTCore"><img src="IOTCORE.png" style="width:100px;">AWS IoT Core Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/HTTPS"><img src="HTTPS.png" style="width:100px;">HTTPS API Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/GRPC"><img src="GRPCLogo.png" style="width:100px;">GRPC Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/WebSocket"><img src="WEBSOCKET.png" style="width:100px;">Web Socket Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/Modbus"><img src="MODBUS.png" style="width:100px;">Modbus TCP Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/OPCUA"><img src="OPCUALogo.png" style="width:100px;">OPC UA Endpoint</a></button></p>
      <p style="color:white;"><button><a href="#/COAP"><img src="COAPLogo.png" style="width:100px;">COAP Endpoint</a></button></p>
      <br>
      <hr>
      <br>
      <h3 style="color:white;">Official SDK Package</h3>
      <p style="color:white;"><button><a href="#/IoTCore"><img src="SDK.png" style="width:100px;">Robomatics IoT SDK</a></button></p>
      <p style="color:white;"><button><a href="#/IoTCore"><img src="API.png" style="width:100px;">Third Party API</a></button></p>
      <br>
      <hr>
      <br>
      <h3 style="color:white;">Developer Support</h3>
      <p style="color:white;"><button><a href="#/Documentation">Documentation</a></button></p>
        <!-- Sidebar content -->
        </div>
    </div>

    <div class="navbar">
        <a href="#/ERP" @click="selectedLevel = 'Level 5 ERP'">Level 5 ERP</a>
        <a href="#/ECommerce" @click="selectedLevel = 'Level 5 ERP'">Level 5 E-Commerce</a>
        <a href="#/WMS" @click="selectedLevel = 'Level 4 WMS'">Level 4 WMS</a>
        <a href="#/MES" @click="selectedLevel = 'Level 4 MES'">Level 4 MES</a>
        <a href="#" @click="selectedLevel = 'Level 3 SCADA/ HMI'">Level 3 SCADA/ HMI</a>
        <a href="#" @click="selectedLevel = 'Level 2 PLC'">Level 2 PLC</a>
        <a href="#" @click="selectedLevel = 'Level 1 Sensor and Actuator'">Level 1 Sensor and Actuator</a>

      <div class="logout">
        <a href="#" @click="logout">Logout</a>
      </div>

      </div>



    <div class="main" style="margin-top:50px; color:white;">
      <h2>IoT Dashboard</h2>
      <br>
      <br>
      <p>Refresh your browser if you're disconnected. Otherwise, you will not get the latest updated data from server</p>
      <table>
          <tr>
            
          <td>Device Number Online</td>
          <td>Total Number Device</td>
          <td>Server Connection</td>
        </tr>
        <tr>
            
            <td>100</td>
            <td>1000</td>
            <td>Offline & Disconnected</td>
          </tr>
      </table>
      <!-- -->
      <p>You can select devices up to 20 for real-time display due to the constraint</p>






      <div>
    <!-- Form -->

        <div v-if="successModalVisible" class="modal">
          <div class="modal-content">
            <h2>Success!</h2>
            <p>Your data has been saved successfully.</p>
            <button @click="closeSuccessModal">Close</button>
          </div>
        </div>
  </div>




  <!-- Confirmation Modal -->
  <div v-if="confirmationModalVisible" class="modal">
      <div class="modal-content">
        <h2>Confirm Delete?</h2>
        <p>Are you sure you want to delete this data?</p>
        <button @click="confirmDelete">Delete</button>
        <button @click="cancelDelete">Cancel</button>
      </div>
    </div>

    
  <br>















    </div>
  </div>



</template>

<script>
import {onMounted, ref} from "vue";
import axios from "axios";
import {useRouter} from "vue-router";
import VueCookies from 'vue-cookies';

export default{
  name: "Home",
  
  data() {
    return{
      formData: {
        name: "",
        email: "",
        // Add more form fields as needed
      },
      showDigitalDropdown: false,
      responseData: null,
      error: null,
      successModalVisible: false,
      userID: 'User123', // Replace 'User123' with your user ID
        userToken: 'UserToken123', // Replace 'UserToken123' with your user token
        plcItems: [
          {
            id: 1,
            name: 'Primary Treatment Plant Tank 1 (OMRON PLC)',
            token: 'Token 1',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '101', description: 'Pressure Alarm', editing: false ,
                  bitAddresses: [
                  {"Bit Address": "101.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "101.15", "Description": "Alarm", "Status": 1},
                  // ... other bitAddresses for this address
                ]
              },
              { name: '102', description: 'pH Alarm', editing: false,
              bitAddresses: [
              { "Bit Address": "102.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "102.15", "Description": "Alarm", "Status": 1},
                  // ... other bitAddresses for this address
              ]},
              { name: '103', description: 'Temperature Alarm', editing: false,
              bitAddresses: [
              {"Bit Address": "100.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.15", "Description": "Alarm", "Status": 1},
                  // ... other bitAddresses for this address
                ]},
              { name: '104', description: 'Level Alarm', editing: false,
                  bitAddresses: [
                  {"Bit Address": "100.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.15", "Description": "Alarm", "Status": 1},
                      // ... other bitAddresses for this address
                ]},
              { name: '105', description: 'Security Alarm', editing: false,
              bitAddresses: [
              {"Bit Address": "100.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.15", "Description": "Alarm", "Status": 1},
                  // ... other bitAddresses for this address
                ]
              },
              { name: '106', description: 'Fire Alarm', editing: false,
              bitAddresses: [
              {"Bit Address": "100.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.15", "Description": "Alarm", "Status": 1},
                  // ... other bitAddresses for this address
                ]},
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 2,
            name: 'Primary Treatment Plant Tank 2 (Siemen PLC)',
            token: 'Token 2',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '0', description: 'Description for Address 1 in PLC 2', editing: false,
              bitAddresses: [
                  {"Bit Address": "100.00", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.01", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.02", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.03", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.04", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.05", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.06", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.07", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.08", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.09", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.10", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.11", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.12", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.13", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.14", "Description": "Alarm", "Status": 1},
                  {"Bit Address": "100.15", "Description": "Alarm", "Status": 1},

                  // ... other bitAddresses for this address
                ]
            },
              { name: '1', description: 'Description for Address 2 in PLC 2', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 3,
            name: 'Primary Treatment Plant Tank 3 (Delta PLC)',
            token: 'Token 3',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '100', description: 'Description for Address 1 in PLC 3', editing: false },
              { name: '101', description: 'Description for Address 2 in PLC 3', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 4,
            name: 'Secondary Treatment Plant Tank 1 (Mitsubushi PLC)',
            token: 'Token 4',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 5,
            name: 'Secondary Treatment Plant Tank 2 (ABB PLC)',
            token: 'Token 5',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 6,
            name: 'Secondary Treatment Plant Tank 3 (Burkert PLC)',
            token: 'Token 6',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 7,
            name: 'Tertiary Treatment Plant Tank 1 (Amsamotion PLC)',
            token: 'Token 7',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '100', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '101', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 8,
            name: 'Tertiary Treatment Plant Tank 2 (HFCA PLC)',
            token: 'Token 8',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '1', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '2', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 9,
            name: 'Tertiary Treatment Plant Tank 3 (Allen Bradley PLC)',
            token: 'Token 9',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '1', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '2', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 10,
            name: 'Advanced Treatment Plant Tank 1 (Schneider PLC)',
            token: 'Token 10',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '1', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '2', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 11,
            name: 'Advanced Treatment Plant Tank 2 (Toshiba PLC)',
            token: 'Token 11',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: '1', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: '2', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          {
            id: 12,
            name: 'Advanced Treatment Plant Tank 3 (Keyence PLC)',
            token: 'Token 12',
            editingToken: false,
            newToken: '',
            showDropdown: false,
            addresses: [
              { name: 'Address 1', description: 'Description for Address 1 in PLC 4', editing: false },
              { name: 'Address 2', description: 'Description for Address 2 in PLC 4', editing: false },
              // Add more addresses with descriptions here
            ],
          },
          // Add more PLC items here as needed
        ],
        newPLCName: '',
        newPLCToken: '',
        newAddress: { name: '', description: '' },
    }
  },
  mounted() {
    // Making a GET request
    axios.get('http://localhost:8089/plc')
      .then(response => {
        this.responseData = response.data;
        for (let i = 0; i < response.data.length; i++) {
          console.log(response.data[i].name);
        }
        //console.log(response.data[0].addresses[0]);
        //console.log(response.data[0].name);
      })
      .catch(error => {
        this.error = error.message;
      });
  },
  methods: {
    showDeleteConfirmation(plcIndex, addressIndex) {
    const confirmed = confirm("Are you sure you want to delete this address?");
    if (confirmed) {
      this.deleteAddress(plcIndex, addressIndex);
    }
  },

  toggleBitAddressVisibility(address, bitIndex) {
      address.bitAddresses[bitIndex].visible = !address.bitAddresses[bitIndex].visible;
    },

    toggleDropdown(plcIndex) {
      this.plcItems[plcIndex].showDigital = false;
      this.plcItems[plcIndex].showAnalog = false;
    },
    toggleAddressDropdown(plcIndex, type) {
      if (type === 'Digital') {
        this.plcItems[plcIndex].showDigital = !this.plcItems[plcIndex].showDigital;
        this.plcItems[plcIndex].showAnalog = false;
      } else if (type === 'Analog') {
        this.plcItems[plcIndex].showAnalog = !this.plcItems[plcIndex].showAnalog;
        this.plcItems[plcIndex].showDigital = false;
      }
    },
//
saveData() {
      // Simulate saving data to the server (replace this with your actual API call)
      // For example, using Axios:
      // axios.post('/api/saveData', this.formData)
      //   .then((response) => {
      //     // Handle success
      //     this.showSuccessModal();
      //     // Clear the form data after successful submission
      //     this.formData = {};
      //   })
      //   .catch((error) => {
      //     // Handle error
      //   });

      // Simulate success for this example
      this.showSuccessModal();
      this.formData = {}; // Clear the form data after successful submission
    },
    showSuccessModal() {
      this.successModalVisible = true;
    },
    closeSuccessModal() {
      this.successModalVisible = false;
    },
    showDigitalDropdown(){
      this.showDigitalDropdown = !this.showDigitalDropdown;
      //showDropdown = true;
      if(showDropdown){
        showDropdown = false;
      }else{
        showDropdown = true;
      }

    },
    fetchOptions() {
      // Simulate fetching JSON data (replace with your actual API call)
      const jsonData = [
        { "id": 1, "name": "Option 1" },
        { "id": 2, "name": "Option 2" },
        { "id": 3, "name": "Option 3" }
      ];
      this.dropdownOptions = jsonData;
    },

//
  
    toggleDropdown(plcIndex) {
          this.plcItems[plcIndex].showDropdown = !this.plcItems[plcIndex].showDropdown;
          //this.plcList[plcIndex].showDigital = !this.plcList[plcIndex].showDigital;
          //this.plcList[plcIndex].showAnalog = !this.plcList[plcIndex].showAnalog;
        },
        deletePLC(plcIndex) {
          this.plcItems.splice(plcIndex, 1);
        },
        addPLC() {
          if (this.newPLCName.trim() !== '' && this.newPLCToken.trim() !== '') {
                  const isDuplicateToken = this.plcItems.some(
                (plcItem) => plcItem.token === this.newPLCToken
              );

              if (isDuplicateToken) {
                // Display an error message or take any action to handle the duplicate token
                alert('Token is already used in another PLC. Please use a different token.');
                return;
              }


            this.plcItems.push({
              id: this.plcItems.length + 1,
              name: this.newPLCName,
              token: this.newPLCToken,
              editingToken: false,
              newToken: '',
              showDropdown: false,
              addresses: [],
            });
            this.newPLCName = '';
            this.newPLCToken = '';
            
          }
        },
        addAddress(plcIndex) {
          if (this.newAddress.name.trim() !== '' && this.newAddress.description.trim() !== '') {
            this.plcItems[plcIndex].addresses.push({
              name: this.newAddress.name,
              description: this.newAddress.description,
              editing: false,
            });
            this.newAddress = { name: '', description: '' };
          }
        },
        deleteAddress(plcIndex, addressIndex) {
          this.plcItems[plcIndex].addresses.splice(addressIndex, 1);
        },
        editAddress(address) {
          address.editing = true;
        },
        saveAddress(address) {
          address.editing = false;
          this.showSuccessModal();

        },
        cancelEdit(address) {
          address.editing = false;
        },
        editPLCToken(plc) {
          plc.editingToken = true;
          plc.newToken = plc.token;
        },

        /*



        */
       savePLCToken(plc) {
      // Check if the new token is not already used in any other PLC
      const isDuplicateToken = this.plcItems.some(
        (plcItem) => plcItem !== plc && plcItem.token === plc.newToken
      );

      if (isDuplicateToken) {
        // Display an error message or take any action to handle the duplicate token
        alert('Token is already used in another PLC. Please use a different token.');
        return;
      }

      plc.token = plc.newToken;
      plc.editingToken = false;
      plc.newToken = '';
      this.showSuccessModal();
    },


        cancelEditPLCToken(plc) {
          plc.editingToken = false;
          plc.newToken = '';
        },

        showDeletePLCConfirmation(plcIndex) {
        const confirmed = confirm("Are you sure you want to delete this PLC?");
        if (confirmed) {
          this.deletePLC(plcIndex);
        }
      },

  },
  created() {
    // Fetch options when the component is created
    this.fetchOptions();
  }
  
}


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
/* Side Menu Dropdown*/

.dropdown {
    position: relative;
    display: inline-block;
  }

  .dropdown-content {
    display: none;
    position: absolute;
    background-color: #f9f9f9;
    color:black;
    min-width: 135px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
  }

  .dropdown:hover .dropdown-content {
    display: block;
  }

  /* Side Menu Dropdown*/

</style>