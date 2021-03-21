<template>
  <div>
    <p class="title"><strong>Place to</strong> visit</p>
    <div class="elevate place box container">
      <img
        classs="box"
        src="https://www.semana.com/resizer/-gDARbwgYKuqVaWiPda5KAYiutU=/1200x675/filters:format(jpg):quality(70)//cloudfront-us-east-1.images.arcpublishing.com/semana/K4YS72T75RF3NPKUE7LZT6AEII.jpg"
        alt=""
      />
      <div class="texto-encima">Medellin, antioquia</div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.container{
    position: relative;
    display: inline-block;
    text-align: center;
}
.texto-encima{
    position: absolute;
    top: 10px;
    left: 10px;
    color: white;
    font-weight: 700;
}
.centrado{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
</style>
