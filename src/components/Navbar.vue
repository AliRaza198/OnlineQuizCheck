<template>
    <nav class="navbar fixed-top d-block">
    <div class="container">
      <div class="internal-section d-flex flex-row justify-content-between w-100 align-items-center">
        <div class="logo align-items-center">
          <a class="navbar-brand" href="#"><img alt="Vue logo" src="../assets/logo.png"> <span class="span1">ACTIVEWEAR</span></a>
        </div>
        <div class="nav-form d-lg-block d-none">
          <form class="d-flex " role="search">
            <input class="form-control me-2" type="search" placeholder="Search..." aria-label="Search" />
            <button class="btn btn-color" type="submit">
              <i class="fa-sharp fa-solid fa-magnifying-glass"></i>
            </button>
          </form>
        </div>
      </div>
    </div>
  </nav>
</template>


<script>
export default{
    name: 'Navbar'
}
</script>


<style scoped>
.navbar{
  background-color: #222629;
}
.logo img{
  height: 50px;
}
.span1{
  color: #86c232;
  font-weight: bold;
}
.btn-color{
  background-color: #86c232;
}
button .fa-magnifying-glass{
  color: white  ;
}
</style>