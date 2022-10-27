

class typeWriting {

  constructor(element) {
    this.element = element; // Selector
    this.words = JSON.parse(element.getAttribute('data-words')); // Input words
    this.speed = parseInt(element.getAttribute('data-speed'), 10) || 100; // fallback 100 ms
    this.delay = parseInt(element.getAttribute('data-delay'), 10) || 1000; // fallback 1000 ms
    this.loop = element.getAttribute('data-loop');
    this.char = ''; // word letters
    this.counter = 0; // loop counter
    this.isDeleting = false; // check when deleting letters
    this.type(); // Typing method
  }

  type() {
    // Set the words index.
    const index = this.loop === 'yes' ? this.counter % this.words.length : this.counter;
    // Get the full word
    const fullWord = this.words[index];
    // Typing speed
    let typeSpeed = this.speed;

    if (this.isDeleting) {
      // Divide speed by 2
      typeSpeed /= 2;
      // Add chars
      this.char = fullWord.substring(0, this.char.length - 1);
    } else {
      // Delete chars
      this.char = fullWord.substring(0, this.char.length + 1);
    }
    // Display on DOM
    this.element.innerHTML = `<span class="write">${this.char}</span><span class="blinking-cursor">|</span>`;
    // When word is completed
    if (!this.isDeleting && this.char === fullWord) {
      // break the loop before deletion.
      if (this.loop === "no" && this.counter >= this.words.length - 1) {
        return;
      }
      // Set char delete to true
      this.isDeleting = true;
      // Set time delay before new word
      typeSpeed = this.delay;
    } else if (this.isDeleting && this.char === '') {
      this.isDeleting = false;
      // Move to next word
      this.counter++;
    }
    // Set time out
    setTimeout(() => this.type(), typeSpeed);

  }

}

// Call the class on DOMContentLoaded
document.addEventListener('DOMContentLoaded', init)
// Select all elements and trigger the class
function init() {
  document.querySelectorAll('.typewrite').forEach(e => new typeWriting(e));
}

class typeWriting{constructor(a){this.element=a,this.words=JSON.parse(a.getAttribute('data-words')),this.speed=parseInt(a.getAttribute('data-speed'),10)||100,this.delay=parseInt(a.getAttribute('data-delay'),10)||1e3,this.loop=a.getAttribute('data-loop'),this.char='',this.counter=0,this.isDeleting=!1,this.type()}type(){const a='yes'===this.loop?this.counter%this.words.length:this.counter,b=this.words[a];let c=this.speed;if(this.isDeleting?(c/=2,this.char=b.substring(0,this.char.length-1)):this.char=b.substring(0,this.char.length+1),this.element.innerHTML=`<span class="write">${this.char}</span><span class="blinking-cursor">|</span>`,!this.isDeleting&&this.char===b){if('no'===this.loop&&this.counter>=this.words.length-1)return;this.isDeleting=!0,c=this.delay}else this.isDeleting&&''===this.char&&(this.isDeleting=!1,this.counter++);setTimeout(()=>this.type(),c)}}document.addEventListener('DOMContentLoaded',init);function init(){document.querySelectorAll('.typewrite').forEach(a=>new typeWriting(a))}

<h1><span class = "typewrite" data-loop = "yes" data-speed = "100" data-delay = "2000" data-words = '["Hello, World!!", "It's PIYUSH-MISHRA-00", "I write Code...,"]'></span></h1>

<p align="center">
        <img src="https://raw.githubusercontent.com/mayhemantt/mayhemantt/Update/svg/Bottom.svg" alt="Github Stats" />
</p>
