<template>
<html>
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

        <!-- <p>This is the sales sheet</p> -->


<section class="form content-wrap">


    <!-- <h2>New Store Location Info</h2> -->

    <form id="new-location">
        <fieldset>
            <legend>Add a new location to the table!</legend>
              <label for="name">Location:</label>
             <input type="text" id="location" required><br>
             <label for="minCustomersPerHour">Minimun number of Customers Per Hour:</label>
             <input type="text" id="minCustomersPerHour" required><br>
             <label for="maxCustomersPerHour">Maximum number of Customers Per Hour:</label>
             <input type="text" id="maxCustomersPerHour" required><br>
             <label for="avgCookiesPerSale" >Average number of Cookies Per Sale: </label>
             <input type="text" id="avgCookiesPerSale" required>

        </fieldset>

          <div>
            <button type="reset">Reset Form</button>
            <button id="submit">Submit New Location</button>
          </div>
    </form>
</section>

        <!-- Display the lists on sales.html.  -->

<div id="table">
<table id="salesData">
    <thead>

    </thead>
    <tbody>

    </tbody>
    <tfoot>

    </tfoot>
</table>

</div>
</main>
<footer>
    <p>We make Salmon Cookies so you don't have to!</p>
            </footer>
        <!-- <script src="../js/app.js"></script> -->
    </body>
</html>
</template>
<script>
import { ref, onMounted } from 'vue'

    const root = ref(null)

    onMounted(() => {
      // the DOM element will be assigned to the ref after initial render
    //   console.log(root.value) // <div>This is a root element</div>
    // })

    'use strict';
console.log ('Hello from the js file');

//global variable
StoreLocation.allStoreLocation=[];


let hours =['6am','7am','8am','9am','10am','11am','12pm','1pm','2pm','3pm','4pm','5pm','6pm','7pm','8pm'];

// Replace all of your object literals for the salmon cookie stand with a single constructor function that,
//  when called with the ‘new’ keyword, it creates a new instance.
// Constructor function
function StoreLocation (location, min, max, avgCookies) {
  this.location = location;
  this.minCustomersPerHour = min;
  this.maxCustomersPerHour = max;
  this.avgCookiesPerSale = avgCookies;
  this.hourlyArray = [];
  this.cookieTotal=0;
  StoreLocation.allStoreLocation.push(this);
}


StoreLocation.prototype.generateCookiesPerHour = function () {
  let min = this.minCustomersPerHour;
  let max = this.maxCustomersPerHour;
  let random = Math.ceil(Math.random() * (max + 1 -min)) +min;
  return random;
};


// Break each column by the hour and complete each row with a “Daily Location Total”.
StoreLocation.prototype.cookiePurchased= function (){
  for (let i = 0; i < hours.length; i++){
    // store hourly cookie totals based on num customers per hour
    this.hourlyArray[i]= Math.floor(this.generateCookiesPerHour() * this.avgCookiesPerSale);
    // daily store cookie total
    let cookieForThisHour = this.hourlyArray[i];
    this.cookieTotal = this.cookieTotal + cookieForThisHour;
    //console.log(this.hourlyArray);
  }
};

StoreLocation.prototype.renderTableData = function () {
  let table = root.value.getElementById('salesData');
  let row = root.value.createElement('tr');

  // city name cell
  let cityNameCell = root.value.createElement('th');
  cityNameCell.textContent = this.location;
  row.appendChild(cityNameCell);

  let tableDataCell;
  // cookie data x 14
  for (let i = 0; i < hours.length; i++) {
    tableDataCell = root.value.createElement('td');
    tableDataCell.textContent = this.hourlyArray[i];
    row.appendChild(tableDataCell);
  }

  tableDataCell = root.value.createElement('td');
  tableDataCell.textContent = this.cookieTotal;
  row.appendChild(tableDataCell);
  table.appendChild(row);
};


// Display each stores data in a table format similar to what is below.
//Create Table head
function renderTableHeaders(){
  let table =root.value.getElementById('salesData');
  let row=root.value.createElement('tr');
  let tableHeadCell=root.value.createElement('th');
  row.appendChild(tableHeadCell);

  //hour of the day headers
  for (let i=0; i<hours.length; i++){
    tableHeadCell=root.value.createElement('th');
    tableHeadCell.textContent=hours[i];
    row.appendChild(tableHeadCell);
  }
  // total header
  tableHeadCell = root.value.createElement('th');
  tableHeadCell.textContent= 'Daily Location Total';
  row.appendChild(tableHeadCell);

  table.appendChild(row);
}
renderTableHeaders();


function renderTableFooter () {
  let table = root.value.getElementById('salesData');
  let row = root.value.createElement('tr');
  let tableFootCell = root.value.createElement('th');
  let hoursOfDay = hours.length;
  tableFootCell.textContent = 'Totals';
  row.appendChild(tableFootCell);

  // to look at 14 hours of the day for 14 totals cells
  for (let i = 0; i < hoursOfDay; i++) {
    let cookieRowTotal = 0;
    // add up cookies from all locations
    for (let j = 0; j < locationInfo.length; j++) {
      cookieRowTotal = cookieRowTotal + locationInfo[j].hourlyArray[i];
    }
    //creates footer cells
    tableFootCell = root.value.createElement('td');
    tableFootCell.textContent = cookieRowTotal;
    row.appendChild(tableFootCell);
  }

  //adds all location totals together into bottom right cell:
  let superTotal = 0;
  for (let i = 0; i < locationInfo.length; i++) {
    superTotal = superTotal + locationInfo[i].cookieTotal;
    //console.log(locationInfo[i].cookieTotal);
  }
  //creates html element
  tableFootCell = root.value.createElement('td');
  tableFootCell.textContent = superTotal;
  row.appendChild(tableFootCell);

  //named this row in order to update later
  row.id = 'footer';
  table.appendChild(row);
}
//  Create function to handle the form submission.
function handleForm(event){
  event.preventDefault();

  let locationElement = root.value.getElementById('location');
  let locationValue = locationElement['value'];

  //IMPORTANT: MAKE SURE THE VALUE INPUTED IN FORM CONVERTS TO A NUMBER:

  let minCustomersPerHourElement = root.value.getElementById('minCustomersPerHour');
  let minCustomersPerHourValue = Number(minCustomersPerHourElement['value']);

  let maxCustomersPerHourElement = root.value.getElementById('maxCustomersPerHour');
  let maxCustomersPerHourValue = Number(maxCustomersPerHourElement['value']);

  let avgCookiesPerSaleElement = root.value.getElementById('avgCookiesPerSale');
  let avgCookiesPerSaleValue = Number(avgCookiesPerSaleElement['value']);



  //remove old totals in footer
  let OldtableTableFooter = root.value.getElementById('footer');
  OldtableTableFooter.remove();

  //create the new location
  // use our constructor
  let newLocation= new StoreLocation(locationValue, minCustomersPerHourValue, maxCustomersPerHourValue, avgCookiesPerSaleValue);
  //update cookies per hour and render new table row
  newLocation.generateCookiesPerHour();
  newLocation.cookiePurchased();
  newLocation.renderTableData();
  //updates table with new totals:
  renderTableFooter();

  // **********Form and Button JS**************
  //make sure form clear out and resets on submit.
  let locationForm=root.value.getElementById('new-location');
  locationForm.reset();
}

// using an array to get info and pass them into constructor
let seattleInfo=new StoreLocation('Seattle', 23, 65, 6.3);
let tokyoInfo=new StoreLocation('Tokoyo', 3, 24, 1.2);
let dubaiInfo=new StoreLocation('Dubai', 11, 38, 3.7);
let parisInfo=new StoreLocation('Paris', 20, 38, 2.3);
let limaInfo=new StoreLocation('Lima', 2,16,4.6);

let locationInfo=[seattleInfo,tokyoInfo, dubaiInfo, parisInfo, limaInfo];

// Replace the lists of your data for each store and build a single table of data instead.
for (let i=0; i<locationInfo.length; i++){
  locationInfo[i].generateCookiesPerHour();
  locationInfo[i].cookiePurchased();
  locationInfo[i].renderTableData();
}
//this renders new information after filling out form
renderTableFooter();


//1. get our element
let locationForm = root.value.getElementById('new-location');
console.log('new-location:', locationForm);
//2. which event am I listening for 'submit'
//add an event listener
locationForm.addEventListener('submit', handleForm);
})
    export default {
      name: 'SalesIndex',
      props: {
        msg: String
      }
    }
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