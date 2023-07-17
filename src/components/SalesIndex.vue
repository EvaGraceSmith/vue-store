<template>
<html ref="root">
    <head>
        <!-- Google fonts -->
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Chicle&family=Josefin+Sans:wght@600&family=Molle&display=swap" rel="stylesheet">
         <!-- Google fonts -->

        <title>sales</title>

        <meta name="description" content="">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="..\css\reset.css">
        <link rel="stylesheet" href="..\css\style.css">
    </head>
    <body>
        <header>
          
            <ul class="navigation-bar">
                <li><a href="#/">Home</a></li>
                <li><a href="#/sales">Sales</a></li>
            </ul>
            <h1 class="logo">The Cookie Stand</h1>
            <img class="salmon" src="../img/salmon.png" alt="Salmon logo">
    </header>


  <main class="sales-page">
    <section class="form content-wrap">
      <form @submit.prevent="addLocation">
        <fieldset>
          <legend>Add a new location to the table!</legend>
          <label for="location">Location:</label>
          <input v-model="newLocation.location" type="text" id="location" required><br>
          <label for="minCustomersPerHour">Minimum number of Customers Per Hour:</label>
          <input v-model="newLocation.minCustomersPerHour" type="text" id="minCustomersPerHour" required><br>
          <label for="maxCustomersPerHour">Maximum number of Customers Per Hour:</label>
          <input v-model="newLocation.maxCustomersPerHour" type="text" id="maxCustomersPerHour" required><br>
          <label for="avgCookiesPerSale">Average number of Cookies Per Sale:</label>
          <input v-model="newLocation.avgCookiesPerSale" type="text" id="avgCookiesPerSale" required>
        </fieldset>

        <div>
          <button type="reset">Reset Form</button>
          <button type="submit">Submit New Location</button>
        </div>
      </form>
    </section>



    <div id="table">
      <table id="salesData">
        <thead>
          <tr>
            <th v-for="header in headers" :key="header">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="row in rows" :key="row.location">
            <td>{{ row.location }}</td>
            <td v-for="sales in row.sales" :key="sales">{{ sales }}</td>
            <td>{{ calculateTotal(row) }}</td>
          </tr>
        </tbody>
      </table>
    </div>
</main>
    <footer>
      <p>We make Salmon Cookies so you don't have to!</p>
    </footer>

</body>
</html>
</template>

<script>
export default {
  data() {
    return {
      newLocation: {
        location: '',
        minCustomersPerHour: '',
        maxCustomersPerHour: '',
        avgCookiesPerSale: ''
      },
      headers: [
        'Location',
        '6AM',
        '7AM',
        '8AM',
        '9AM',
        '10AM',
        '11AM',
        '12PM',
        '1PM',
        '2PM',
        '3PM',
        '4PM',
        '5PM',
        '6PM',
        '7PM',
        '8PM',
        'Daily Location Total'
      ],
      rows: []
    };
  },
  mounted() {
    this.generateTableRows();
  },
  methods: {
    addLocation() {
      // Add the new location to the table
      let newRow = {
        location: this.newLocation.location,
        minCustomersPerHour: this.newLocation.minCustomersPerHour,
        maxCustomersPerHour: this.newLocation.maxCustomersPerHour,
        avgCookiesPerSale: this.newLocation.avgCookiesPerSale,
        sales: []
      };

      for (let i = 0; i < 15; i++) {
        newRow.sales.push(this.getRandomNumber(20, 80));
      }

      newRow.sales.push(this.calculateTotal(newRow));
      this.rows.push(newRow);

      // Reset the form
      this.newLocation = {
        location: '',
        minCustomersPerHour: '',
        maxCustomersPerHour: '',
        avgCookiesPerSale: ''
      };
    },

    generateTableRows() {
      let locations = ['Seattle', 'Tokyo', 'Dubai', 'Paris', 'Lima'];

      for (let i = 0; i < locations.length; i++) {
        let row = {
          location: locations[i],
          sales: []
        };

        for (let j = 0; j < 15; j++) {
          row.sales.push(this.getRandomNumber(20, 80));
        }

        this.rows.push(row);
      }
    },
    calculateTotal(row) {
      let total = 0;

      for (let i = 0; i < row.sales.length; i++) {
        total += parseInt(row.sales[i]);
      }

      return total;
    },
    getRandomNumber(min, max) {
      return Math.floor(Math.random() * (max - min + 1) + min);
    }
  }
};
</script>


    
    <!-- Add "scoped" attribute to limit CSS to this component only -->
    
    <style scoped>
    
    /* Color Palette
    Base color: Salmon #fa8072;
    Dark Salmon #a03a2f;
    Medium Salmon: #FFA49A;
    Light Salmon:  #FFC9C3;
    Lightest Salmon #fee0dd;
    Complementary Color: Green- GB [hex]	#56BD6D;
    dark green: #1C8B35
    Quad Apricot:  #FAB472;
    Dark Apricot: #92541b;
    Quad  Dusty Blue:  #488D9A; 
    dark Dusty Blue: #196371;
    Light Gray:  rgb(205, 199, 198);
    Dark Gray :  rgb(73, 56, 54);
    Whitesmoke:  whitesmoke;
    font-family: 'Chicle', cursive;
    font-family: 'Josefin Sans', sans-serif;
    font-family: 'Molle', cursive;
    */
    
    /* *********************************Global Styles****************************** */
    body {
        background-color: white;
    
    }
    header {
        background: #196371;
    height: 150px;
    color: whitesmoke;
    
    
    }
    .navigation-bar {
        list-style-type: none;
        padding: 10px;
        display: flex;
        justify-content: right;
        text-align: right;
        font-size: 20px;
        font-family: 'Josefin Sans', sans-serif;
      }
      
    .navigation-bar a {
        padding: 15px;
        text-decoration: none;
        color: whitesmoke;
        text-align: right;
      }
    
      .logo-words{
        position: absolute;
        padding-top: -30px;
      }
    
      .content-wrap {
        max-width: 1000px;
        width: 85%;
        margin: 0 auto;
        /* padding: 60px 0; */
        }
    
      .logo {
        color: whitesmoke;
        font-size: 40px;
        text-align: left;
        margin-top: -10px;
        margin-bottom: -8px;
        padding-left: 30px;
        font-family: 'Chicle', cursive;
      }
    
      .salmon {
        height: 50px;
        padding-left: 61px;
        padding-top: 5px;
      }
    
    main {
        /* height: 2000px; */
        background-color: white;
    }
    
    h1, h2, h3{
        color: #196371;
    }
    
    
    
    footer {
        background: #196371;
        height: 150px;
        color: whitesmoke;
    }
    /* *********************************index.HTML****************************** */
    
    .intro {
     background-image: url("../img/mockaroon-bzLhhI3MpYY-unsplash.jpg");
     background-size: cover;
     height: 600px;
    
    }
    
    
    
    /* ******************about us**************** */
    
    
    
    
    .family-photo{
      display: flex;
      align-items: center;
    border-radius: 30px;
    max-width: 900px;
    width: 85%;
    margin: 0 auto;
    padding: 60px 0;
    
    }
    
    .family-photo>img{
      border: 3px #FFC9C3;
      border-radius: 30px;
      box-shadow: 0 3px 10px black;
    }
    
    .heading {
    padding-top: 20px;
    font-family: 'Chicle', cursive;
    font-size: 40px;
    padding-bottom: 20px;
    color: #196371;
    
    }
    
    
    .our-family {
      flex: 1 480px;
      border-radius: 10px;
    }
    
    
    .scroll{
      overflow-y:scroll;
      width: 480 px;
      height: 300px;
      border:1px solid #196371;
      box-shadow: 0 3px 10px #196371;
      border-radius: 10px;
      padding: 10px;
      background-color: #ffebe9;
      font-family: 'Josefin Sans', sans-serif;
      font-size: 22px;
      line-height: 1.5;
      max-width: 800px;
      width: 85%;
      margin: 0 auto;
      margin-bottom: 100px;
    
    }
    
    article:nth-of-type(2) div:first-child {
      /* flex: 1 50px; */
      display: flex;
      flex-flow: row wrap;
      align-items: center;
      justify-content: space-around;
    }
    
    
    /* ******************shop**************** */
    
    .trio{
      display: flex;
      /* max-width: 900px; */
      width: 85%;
      margin: 0 auto;
        /* margin: 30px; */
        max-width: 1000px;
        width: 85%;
        margin: 0 auto;
    
    }
    
    .box1 img{
      width: 300px;
      height: auto;
      vertical-align: middle;
      justify-content: center;
      object-fit: contain;
    }
    
    .box2 img{
      width: 300px;
      height: auto;
      justify-content: center;
      object-fit: contain;
    }
    
    .box3 img{
      width: 300px;
      height: auto;
      justify-content: center;
      object-fit: contain;
    }
    .box1 {
      height: 350px;
      width: 300px;
      background-color: white;
      box-sizing: border-box;
      margin-top:30px;
      margin-bottom:30px;
      margin-right:30px;
      box-shadow: 0 3px 10px black;
      justify-content: center;
      vertical-align: middle;
      display: flex;
    }
    .box2 {
      height: 350px;
      width: 300px;
      background-color: white;
      box-sizing: border-box;
      margin:30px;
      box-shadow: 0 3px 10px black;
      display: flex;
    }
    .box3 {
      height: 350px;
      width: 300px;
      background-color: white;
      box-sizing: border-box;
      margin:30px;
      box-shadow: 0 3px 10px black;
      display: flex;
    }
    
    /* ******************locations**************** */
    .hours{
      font-family: 'Josefin Sans', sans-serif;
    text-align: center;
    }
    .hours > h1 {
      font-size: 25px;
      line-height: 2;
    }
    .hours > h3{
      font-size: 30px;
      padding-bottom: 40px;
    }
    .store-info{
      height: 600px;
      background-color: #196371;
    }
    
    h2 {
      font-size: 20px;
      text-align: center;
    }
    
    /* Add your flexbox CSS below here */
    
    .locations {
      display: flex;
      font-family: 'Josefin Sans', sans-serif;
      line-height: 1.5;
      height: 200px;
      max-width: 960px;
      justify-content:center;
      margin-left: 35px;
      /* border: 1px solid #2d2d2d; */
    
    }
    .locations >article {
      padding: 10px;
      margin: 10px;
      padding-left: 20px;
      background-color:#c2e6ed;
      flex: 1;
      box-shadow: 0 3px 10px #196371;
      
    }
    
    footer>p {
      font-size: 40px;
      text-align: center;
      padding-top: 60px;
      font-family: 'Chicle', cursive;
      text-shadow: 1px 1px 1px #488D9A;
    }
    
    
    /* *********************************Sales.HTML****************************** */
    .sales-page{
      height: 1000px;
    }
    
    /* *********************************Form****************************** */
    
    input[type=text], select {
      width: 50%;
      padding: 12px 20px;
      margin: 8px 0;
      display: inline-block;
      border: 2px solid #196371;
      border-radius: 4px;
      box-sizing: border-box;
    }
    
    input[type=submit] {
      width: 50%;
      background-color: red;
      color: white;
      padding: 14px 20px;
      margin: 8px 0;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    
    input[type=submit]:hover {
      background-color: blue;
    }
    
    .form {
    text-align: center;
      max-width: 700px;
      width: 85%;
      margin: 0 auto;
      margin-top: 50px;
      margin-bottom: 50px;
      border-radius: 10px;
      background-color:   #80bfcc; 
      padding: 20px;
      font-family: 'Josefin Sans', sans-serif;
      box-shadow: 0 3px 10px #196371;
    }
    
    
    legend {
      color:dark #196371;
      font-family: 'Josefin Sans', sans-serif;
      font-size: 20px;
    
    }
    
    button {
      background-color:#d2eaef;
      margin-top: 15px;
      font-family: 'Josefin Sans', sans-serif;
      font-size: 18px;
      line-height: 1.5;
      border-radius: 10px;
    }
    button:hover {
      background-color: rgb(36, 128, 133);
      color: whitesmoke;
    
    }
    
    
    
    /* *********************************Table****************************** */
    
    
    .sales {
        background-color: salmon;
        color: #a03a2f; 
    }
    
    #table{
      display: flex;
      width: 1000px;
      margin: auto;
      padding-right:20px;
    
    }
    #salesData  {
    
        color: #a03a2f;
        list-style-position: inside;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
        margin-top: 30px;
        font-family: 'Josefin Sans', sans-serif;
      
    }
    
    table {
      border-radius: 30px;
      border: 5px solid #fa8072 ;
      border-collapse: collapse; 
     
      width: 100%;
      background-color: #ffebe9;
    
    }
    
    th, td, tfoot {
        padding: 10px;
        text-align: center;
        border: 2px solid #fa8072;
    }
      tr:hover    {background-color: #FFA49A;}
    
    /* *********************************Shop CSS****************************** */
    .shopMain{
      height: 2000px;
    }
    
    </style>