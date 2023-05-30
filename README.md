# splash
## <img width="1187" alt="Screenshot 2023-05-29 at 6 12 12 PM" src="https://github.com/sudo-self/splash/assets/119916323/5e0d9b6f-fe9c-44e4-9863-88cd843810a3">
## <img width="1275" alt="Screenshot 2023-05-29 at 6 18 17 PM" src="https://github.com/sudo-self/splash/assets/119916323/cae88328-0873-4a80-a956-517ce35fcdda">
### 
</head>
<body>
<sectio class="nav">
  <h1>THE DEVELOPER</h1>
  <div class="nav-container"><a class="nav-tab" href="#tab-svelte">The Domain</a><a class="nav-tab" href="#tab-esbuild">BTC Wallet</a><a class="nav-tab" href="#tab-next">Snake II</a><a class="nav-tab" href="#tab-typescript">The Shelf</a><a class="nav-tab" href="#tab-vite">Retro Games</a><span class="nav-tab-slider"></span></div>
</sectio>
<main class="main">
  <section class="slider" id="tab-svelte">
    <h1>The Domain</h1>
    <h2><a href="https://JesseJesse.com">JesseJesse.com</a></h2>
  </section>
  <section class="slider" id="tab-esbuild">
    <h1>BTC wallet</h1>
    <h2><a href="https://crypto.JesseJesse.com">crypto.JesseJesse.com</h2>
  </section>
  <section class="slider" id="tab-next">
    <h1>Snake II</h1>
    <h2><a href="https://snake2.JesseJesse.com">snake2.JesseJesse.com</h2>
  </section>
  <section class="slider" id="tab-typescript">
    <h1>The Shelf</h1>
    <h2><a href="https://shop.JesseJesse.com">shop.JesseJesse.com</h2>
  </section>
  <section class="slider" id="tab-vite">
    <h1>Retro Gaming</h1>
    <h2><a href="https://Java.JesseJesse.com">Java.JesseJesse.com</h2>
  </section>
</main>
<canvas class="background"></canvas>
</body>
</html>
<img width="330" alt="Screenshot 2023-05-29 at 6 14 55 PM" src="https://github.com/sudo-self/splash/assets/119916323/1c7db120-61c8-4575-a488-3899a565a13f">

window.onload = function () {
  Particles.init({
    selector: ".background"
  });
};
const particles = Particles.init({
  selector: ".background",
  color: ["#03dac6", "#ff0266", "#000000"],
  connectParticles: true,
  responsive: [
    {
      breakpoint: 768,
      options: {
        color: ["#faebd7", "#03dac6", "#ff0266"],
        maxParticles: 43,
        connectParticles: false
      }
    }
  ]
});

class NavigationPage {
  constructor() {
    this.currentId = null;
    this.currentTab = null;
    this.tabContainerHeight = 70;
    this.lastScroll = 0;
    let self = this;
    $(".nav-tab").click(function () {
      self.onTabClick(event, $(this));
    });
    $(window).scroll(() => {
      this.onScroll();
    });
    $(window).resize(() => {
      this.onResize();
    });
  }

  onTabClick(event, element) {
    event.preventDefault();
    let scrollTop =
      $(element.attr("href")).offset().top - this.tabContainerHeight + 1;
    $("html, body").animate({ scrollTop: scrollTop }, 600);
  }

  onScroll() {
    this.checkHeaderPosition();
    this.findCurrentTabSelector();
    this.lastScroll = $(window).scrollTop();
  }

  onResize() {
    if (this.currentId) {
      this.setSliderCss();
    }
  }

  checkHeaderPosition() {
    const headerHeight = 75;
    if ($(window).scrollTop() > headerHeight) {
      $(".nav-container").addClass("nav-container--scrolled");
    } else {
      $(".nav-container").removeClass("nav-container--scrolled");
    }
    let offset =
      $(".nav").offset().top +
      $(".nav").height() -
      this.tabContainerHeight -
      headerHeight;
    if (
      $(window).scrollTop() > this.lastScroll &&
      $(window).scrollTop() > offset
    ) {
      $(".nav-container").addClass("nav-container--move-up");
      $(".nav-container").removeClass("nav-container--top-first");
      $(".nav-container").addClass("nav-container--top-second");
    } else if (
      $(window).scrollTop() < this.lastScroll &&
      $(window).scrollTop() > offset
    ) {
      $(".nav-container").removeClass("nav-container--move-up");
      $(".nav-container").removeClass("nav-container--top-second");
      $(".nav-container-container").addClass("nav-container--top-first");
    } else {
      $(".nav-container").removeClass("nav-container--move-up");
      $(".nav-container").removeClass("nav-container--top-first");
      $(".nav-container").removeClass("nav-container--top-second");
    }
  }

  findCurrentTabSelector(element) {
    let newCurrentId;
    let newCurrentTab;
    let self = this;
    $(".nav-tab").each(function () {
      let id = $(this).attr("href");
      let offsetTop = $(id).offset().top - self.tabContainerHeight;
      let offsetBottom =
        $(id).offset().top + $(id).height() - self.tabContainerHeight;
      if (
        $(window).scrollTop() > offsetTop &&
        $(window).scrollTop() < offsetBottom
      ) {
        newCurrentId = id;
        newCurrentTab = $(this);
      }
    });
    if (this.currentId != newCurrentId || this.currentId === null) {
      this.currentId = newCurrentId;
      this.currentTab = newCurrentTab;
      this.setSliderCss();
    }
  }

  setSliderCss() {
    let width = 0;
    let left = 0;
    if (this.currentTab) {
      width = this.currentTab.css("width");
      left = this.currentTab.offset().left;
    }
    $(".nav-tab-slider").css("width", width);
    $(".nav-tab-slider").css("left", left);
  }
}

new NavigationPage();



