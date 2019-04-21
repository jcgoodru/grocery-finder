<template>
  <div>
    <input id="pac-input" class="controls m-2 px-2" type="text" placeholder="Enter Address...">
  </div>
</template>

<script>
export default {};
</script>

<style>
    #pac-input {
      background-color: #fff;
      font-family: Roboto;
      font-size: 15px;
      font-weight: 300;
      text-overflow: ellipsis;
      width: 80%;
    }
    #pac-input:focus {
      border-color: #4d90fe;
    }
</style>
