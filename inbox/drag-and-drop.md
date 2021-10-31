https://codepen.io/tibo3000/pen/yMpBXV
```html
<div class="wrapper">
<div class="drag" data-target=".drop">
  <div class="dragtext">
  drag me
  </div>
</div>

<div class="drop">
  <div class="droptext">
    dropped
  </div>
</div>
  <div class="debug"></div>
</div>
```

```css
@keyframes bye {
  0% {
    transform: scale(1) rotate(-1deg)
  }
  50% {
    transform: scale(1.1) rotate(-2deg)
  }
  100% {
    transform: scale(0) rotate(3deg)
  }
}

@keyframes begindrag {
  0% {
    transform: rotate(0deg)
  }
  10% {
    transform: rotate(-8deg)
  }
  30% {
    transform: rotate(6deg)
  }
  55% {
    transform: rotate(-3deg)
  }
  80% {
    transform: rotate(1deg)
  }
  100% {
    transform: rotate(-1deg)
  }
}

.wrapper{
  user-select:none;
}

.drop {
  float:right;
  position: relative;
  margin: 10px;
  width: 400px;
  height: 200px;
  border: 5px dashed #ff5722;
  border-radius:15px;
  background: white;
  transition: background .4s ease;
}
.drag {
  position:relative;
  margin: 10px;
  width: 400px;
  height: 200px;
  background: #ff5722;
  border-radius:15px;
  cursor:move;
  z-index:30;
  transition: opacity .3s ease, transform .6s ease;
}

.beginDrag {
  animation: begindrag .8s ease forwards;
}
.dragged {
  position: absolute;
  box-shadow: 0 0 20px rgba(255,255,255,0.8);
  transform: rotate(-1deg);
  opacity: 0.5;
  tranistion: all .3s ease;
}
.readyDrop {
  opacity:0.8 !important;
  transition: opacity .3s ease;
}
.bye {
  opacity: 1;
  transition: opacity .5s ease;
  animation: bye .4s ease forwards;
}

.dragtext,.droptext {
  font-family:'Helvetica';
  font-weight: 900;
  color:#FFF;
  font-size:50px;
  text-align:center;
  line-height: 190px;
}
```

```javascript
var isDragging = false;
var previousX = 0;

// called after dropping animation is completed
function onDrop () {
  $('.drop').css({'background':'#ff5722'})
  window.setTimeout(function () {
    $('.drop').css({'background':'white'})
  }, 2500);
}

// collision detection
// source : http://stackoverflow.com/questions/4230029/jquery-javascript-collision-detection
function isColliding (x, y, element2) {
    var e2 = {};
    e2.top = $(element2).offset().top;
    e2.left = $(element2).offset().left;
    e2.right = parseFloat($(element2).offset().left) + parseFloat($(element2).width());
    e2.bottom = parseFloat($(element2).offset().top) + parseFloat($(element2).height());

    if (x > e2.left && x < e2.right && y < e2.bottom && y > e2.top) {
        return true
    }
}

$('.drag').on('mousedown', function (e) {
  var isDragging = true;
  var drag = $(this).clone().addClass('dragged').appendTo('.wrapper');
  var dropZone = $(this).data('target');
  var originalPosX = $(this).offset().left;
  var originalPosY = $(this).offset().top;
  var startX = e.clientX - originalPosX;
  var startY = e.clientY - originalPosY;
  drag.css({'left':e.clientX - startX, 'top': e.clientY - startY})
  drag.css({'transform-origin': Math.round(startX / drag.outerWidth() * 100) + '% ' + Math.round(startY / drag.outerHeight() * 100) + '%'})
  drag.addClass('beginDrag')
  $(window).on('mousemove', function (event) {
    if (isDragging) {
      drag.css({'left':event.clientX - startX, 'top': event.clientY - startY})
      if (isColliding(event.clientX, event.clientY, '.drop')) {
        drag.removeClass('beginDrag')
        drag.addClass('readyDrop')
      } else {
        drag.removeClass('readyDrop')
      }
    }
  });
  $(window).on('mouseup', function (event) {
    if (isDragging) {
      $(window).off('mousemove');
      if (isColliding(event.clientX,event.clientY,'.drop')) {
        drag.removeClass('readyDrop').addClass('bye');
        
        window.setTimeout(function () {
          onDrop()
        drag.remove()
      }, 400)
      } else {
        drag.animate({'top':originalPosY, 'left':originalPosX, 'opacity': 0}, 400, function () {
          drag.remove()
        })
      }
      isDragging = false;
    }
  })
});
```
