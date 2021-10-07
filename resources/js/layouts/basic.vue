<template>
  <!-- <div class="basic-layout d-flex align-items-center justify-content-center m-0 bg-white">
    <child />
  </div> -->
  <div id="main-wrapper">

        <!--**********************************
            Nav header start
        ***********************************-->
        <div class="nav-header">
            <a href="" class="brand-logo">

                <img class="logo-compact" src="'images/logo-text.png'" alt="">
                <img class="brand-title" src="'images/logo-text.png'" alt="">

            </a>

            <div class="nav-control">
                <div class="hamburger">
                    <span class="line"></span><span class="line"></span><span class="line"></span>
                </div>
            </div>
        </div>
        <!--**********************************
            Nav header end
        ***********************************-->

        <!--**********************************
            Chat box start
        ***********************************-->
        <!-- @include('elements.chat-box') -->
        <!--**********************************
            Chat box End
        ***********************************-->

        <!--**********************************
            Sidebar start
        ***********************************-->
        <!-- @include('elements.sidebar') -->
        <!--**********************************
            Sidebar end
        ***********************************-->

        <!--**********************************
            Header start
        ***********************************-->

          <!-- @include('elements.header') -->


        <!--**********************************
            Header end ti-comment-alt
        ***********************************-->

        <!--**********************************
            Content body start
        ***********************************-->
        <div class="content-body">
            <!-- row -->
            <!-- @yield('content') -->
             <child />
        </div>
        <!--**********************************
            Content body end
        ***********************************-->


        <!--**********************************
            Footer start
        ***********************************-->

		<!-- @include('elements.footer') -->

        <!--**********************************
            Footer end
        ***********************************-->

		<!--**********************************
           Support ticket button start
        ***********************************-->

        <!--**********************************
           Support ticket button end
        ***********************************-->


    </div>
</template>

<script>
export default {
  name: 'BasicLayout'
}
</script>

<style lang="scss">
.basic-layout {
  color: #636b6f;
  height: 100vh;
  font-weight: 100;
  position: relative;

  .links > a {
    color: #636b6f;
    padding: 0 25px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: .1rem;
    text-decoration: none;
    text-transform: uppercase;
  }
}
</style>
