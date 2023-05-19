<template>
    <div class="sidebar">
    <div class="logo_details">
      <i class="bx bx-menu" id="btn"></i>
    </div>
    <ul class="nav-list">
      <li class="d-lg-none d-block">
        <i class="bx bx-search"></i>
        <input type="text" placeholder="Search...">
      </li>
      <li>
        <a href="#">
          <i class="bx bx-grid-alt"></i>
          <span class="link_name">Dashboard</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="bx bx-user"></i>
          <span class="link_name">User</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="bx bx-chat"></i>
          <span class="link_name">Message</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="bx bx-folder"></i>
          <span class="link_name">File Manger</span>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: "Sidebar"
};
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

*{
  padding: 0%;
  margin: 0%;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}
.sidebar{
  min-height: 100vh;
  width: 78px;
  padding: 6px 14px;
  z-index: 99;
  background-color: #474b4f;
  transition: all .5s ease;
  position: fixed;
  top:54px;
  left: 0;
}
.sidebar.open{
  width: 250px;
}
.sidebar i{
  color:white;
  height: 60px;
  line-height: 60px;
  min-width: 50px;
  font-size: 25px;
  text-align: center;
}
.sidebar ul li{
  position: relative;
  margin-top:8px;
  list-style: none;
}
ul i{
  background-color: #61892f;
}

.sidebar input{
  font-size: 15px;
  color:#474b4f;
  font-weight: 400;
  outline: none;
  height: 33px;
  width: 35px;
  border:none;
  border-radius: 5px;
  background-color: #86c232;
  transition: all .5s ease;
}

.sidebar input::placeholder{
  color:#474b4f;
}
.sidebar.open input{
  width: 100%;
  padding: 0 20px 0 50px;
}
.sidebar .bx-search{
  position: absolute;
  top:50%;
  left:0;
  transform: translateY(-50%);
  font-size: 22px;
  background-color: #61892f ;
  color: #fff;
}
.sidebar li a{
  display: flex;
  height: 100%;
  width: 100%;
  align-items: center;
  text-decoration: none;
  background-color: #86c232;
  position: relative;
  transition: all .5s ease;
  border-radius: 5px;
  z-index: 12;
}
.sidebar li a .link_name{
  color:#474b4f;
  font-size: 15px;
  font-weight: 400;
  white-space: nowrap;
  pointer-events: auto;
  transition: all 0.4s ease;
  pointer-events: none;
  opacity: 0;
}
.sidebar.open li a .link_name{
  opacity: 1;
  pointer-events: auto;
}
.sidebar li i{
  height: 35px;
  line-height: 35px;
  font-size: 18px;
  border-radius: 5px;
}
.home-section{
  position: relative;
  background-color:#e4e9f7;
  min-height: 100vh;
  top:54px;
  left:78px;
  width: calc(100% - 78px);
  transition: all .5s ease;
  /* z-index: 2; */
}

.home-section .text{
  display: inline-block;
  color:#004f83;
  font-size: 25px;
  font-weight: 500;
  margin: 18px;
}

.sidebar.open ~ .home-section{
  left:250px;
  width: calc(100% - 250px);
}
.column{
  display: flex;
}
.container{
  margin: 0px;
  background-color: chocolate;
}
</style>
