<template>
  <router-view/>
</template>

<style lang="scss">
body {
 margin: 0;

 font-family: 'Lato', sans-serif;
 background: #fff;
 font-size: 15px;

 color: #000;
 -webkit-font-smoothing: antialiased;

}

h1, h2, h3, h4, h4, h5 {
 margin: 0;
}

*,
*:before,
*:after {
 box-sizing: border-box;
}

.container {
 width: 100%;
 max-width: 1284px;
 margin: 0 auto;
 padding: 0 10px;
}

.header {
  text-align: center;
  margin: 40px 0;
}

.btn {
 display: inline-block;
 position: relative;
 font-weight: 700;
 text-decoration: none;
 padding: 10px 20px;
 font-size: 16px;
 line-height: 19px;
 transition: all .2s ease;
 color: #fff;
 background: #006DFE;
 cursor: pointer;
 border: none;
 border-radius: 1px;

 &::before {
  position: absolute;
  content: '';
  background: #fff;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform: scaleY(0);
  transition: all .2s ease;
  z-index: 1;
  border: 1px solid #006DFE;
 }

 &:hover {
  color: #006DFE;
  &::before {
   transform: scaleY(1);
  }
 }

 &:focus {
  transform: scale(.95);
 }

 span {
  position: relative;
  z-index: 2;
 }
}

</style>
