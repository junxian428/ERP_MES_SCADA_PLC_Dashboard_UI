<template>
    <div>
      <div v-for="item in jsonData" :key="item.id">
        <div @click="toggleDropdown('both', item.id)" class="row">
          {{ item.name }}
        </div>
        
        <div v-if="item.showAnalogAndDigital" class="dropdown">
                    <!---->


                    <div @click="toggleDropdown('digital', item.id)" class="row">
                        Digital

                    </div>
                        <div v-if="item.showDigitalDropdown" class="dropdown">


                        <div @click="toggleDropdown('bitaddress', item.id)">Digital: {{ item.digital }}</div>

                        
                        <div v-if="item.showBitAddress" class="dropdown">
                            This is bit Address
                        </div>

                        <!---->
                        <div v-if="item.showAnalogDropdown" class="dropdown">
                            Analog: {{ item.analog }}
                        </div>


                    </div>
                    <!---->

                    <div @click="toggleDropdown('analog', item.id)" class="row">
                        Analog
                    </div>

                    <div v-if="item.showAnalogDropdown" class="dropdown">
                    Analog: {{ item.analog }}
                    </div>
     
        </div>
  
 

      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        bitAddress: [
            {bitAddress: 100.00},
            {bitAddress: 100.00},
        ],
        jsonData: [
          { id: 1, name: 'PLC 1', analog: 'Analog 1', digital: 'Digital 1', showAnalogDropdown: false, showDigitalDropdown: false, showAnalogAndDigital: false, showBitAddress: false },
          { id: 2, name: 'PLC 2', analog: 'Analog 2', digital: 'Digital 2', showAnalogDropdown: false, showDigitalDropdown: false, showAnalogAndDigital: false, showBitAddress: false },
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
            this.jsonData[index].showBitAddress = !this.jsonData[index].showBitAddress;
          }
        }
      },
    },
  };
  </script>
  
  <style>
  /* Add your CSS styling here */
  </style>
  