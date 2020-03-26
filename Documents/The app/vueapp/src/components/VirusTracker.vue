<template>
    <div class="container">
        <img id="flag" src ="https://raw.githubusercontent.com/NovelCOVID/API/master/assets/flags/cn.png"/>;
    </div>
</template>

<script>


let new_cases = document.getElementById("new_case");
let new_death = document.getElementById("new_death");
let total_death = document.getElementById("total_death");
let total_recovered = document.getElementById("total_recovered");
let total_cases = document.getElementById("total_cases");
let table = document.getElementById('countries_stat');

fetch("https://coronavirus-monitor.p.rapidapi.com/coronavirus/worldstat.php", {
    "method": "GET",
    "headers": {
        "x-rapidapi-host": "coronavirus-monitor.p.rapidapi.com",
        "x-rapidapi-key": "53009286a0mshdc8ec356f7aa205p1e0e80jsn5858f548ed53"
    }
})
.then(response => response.json().then( data => {
    console.log(data);
    total_cases.innerHTML = data.total_cases;
    new_cases.innerHTML = data.new_cases;
    new_death.innerHTML = data.new_deaths;
    total_death.innerHTML = data.total_deaths;
    total_recovered.innerHTML = data.total_recovered;

})).catch(err => {
    console.log(err);
});

let country = document.createElement("country");
let link = document.createElement("link");
fetch("https://corona.lmao.ninja/countries")
.then(response => response.json().then(data =>{
    console.log(data);
    let countries_stat = data;
//Getting all the country statistic using a loop
    for (let i = 0; i<countries_stat.length;i++){
        console.log(countries_stat[i]);
        //we will start by inserting the new rows inside our table
        let row = table.insertRow(i+1);
        country = row.insertCell(0);
        let cases = row.insertCell(1);
        let todayCases = row.insertCell(2);
        let deaths = row.insertCell(3);
        let todayDeaths = row.insertCell(4);
        let recovered = row.insertCell(5);
        let active = row.insertCell(6);
        let critical = row.insertCell(7);
        let casesPerOneMillion = row.insertCell(8);
        let deathsPerOneMillion = row.insertCell(9);

        let countryInfo = countries_stat[i].countryInfo;
        link = countryInfo.flag;

        country.innerHTML = countries_stat[i].country + "<br>";

        var img = new Image();
        img.src = link;
        country.appendChild(img);

        cases.innerHTML = countries_stat[i].cases;
        todayCases.innerHTML = countries_stat[i].todayCases;
        deaths.innerHTML = countries_stat[i].deaths;
        todayDeaths.innerHTML = countries_stat[i].todayDeaths;
        recovered .innerHTML = countries_stat[i].recovered ;
        active.innerHTML = countries_stat[i].active;
        critical.innerHTML = countries_stat[i].critical;
        casesPerOneMillion.innerHTML = countries_stat[i].casesPerOneMillion;
        deathsPerOneMillion.innerHTML = countries_stat[i].deathsPerOneMillion;
    }
}))
.catch(err => {
    console.log(err);
});


</script>


<style>
  h3 {
    margin-bottom: 5%;
  }
</style>
