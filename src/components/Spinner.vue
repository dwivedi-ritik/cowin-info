<template>
    <div class="spinner" >
        <div class="spin-center">
            <div class="spin"></div>
        </div>
    </div>
</template>

<style>
.spinner{
    width: 100vw;
    height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
}
.spin{
    display: block;
    width:40px;
    height: 40px;
    border:3px solid transparent;
    border-radius: 50%;
    border-top-color: blueviolet;
    animation: spin 1s ease-in infinite;
}
@keyframes spin {
    to { transform: rotateZ(360deg) }
}

</style>