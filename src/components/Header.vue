<template>
  <div class="head-info">
        <p>Daily Vaccination Information</p><br>
        <div class="head-detail-in">
            <p id="head-text">Source of data is <a href="https://dashboard.cowin.gov.in/" id="link">Cowin-portal </a>, 
                click at Cowin text for more information.i know site is incomplete in many but i made it just as pratice project. 
                Details at the side of arrow shows the current increased data </p>
        </div>
    </div>
</template>


<style>
#head-text{
    color: dimgrey;
    font-size:14px;
    line-height: 18px;
}
.head-info{
    margin-top: 3%;
    width: 100vw;
    height: 100px;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}
.head-detail-in{
    height: 180px;
    width: 450px;
}
</style>