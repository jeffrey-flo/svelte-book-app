<script >
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";

  let cart = [];
  function addToCart() {
    cart = [...cart, 'svelte-book'];
  }

  let product = {
    id: "svelte-book",
    name: "Svelte Guide",
    price: 30000,
    images: [
      "https://github.com/developer-book/svelte/blob/main/static/svelte-book-1.png?raw=true",
      "https://github.com/developer-book/svelte/blob/main/static/svelte-book-2.png?raw=true",
      "https://github.com/developer-book/svelte/blob/main/static/svelte-book-3.png?raw=true",
    ],
  };

  let sliderCenterIndex = 0;
  let sliderLeftIndex = product.images.length - 1;
  let sliderRightIndex = 1;

  function sliderMoveLeft(){
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex - 1 + length) % length;
    sliderLeftIndex = (sliderCenterIndex - 1 + length) % length;
    sliderRightIndex = (sliderCenterIndex + 1) % length;
  }
  function sliderMoveRight(){
    const length = product.images.length;
    sliderCenterIndex = (sliderCenterIndex + 1) % length;
    sliderLeftIndex = (sliderCenterIndex - 1 + length) % length;
    sliderRightIndex = (sliderCenterIndex + 1) % length;
  }



  let releatedProducts = [
    {
      id: "react-book",
      name: "React Guide",
      price: 30000,
    }
  ];

</script>

<header class="header">
  <a class="header-title" href="/">Svelte Site</a>
  <nav>
    <ul class="header-links">
      <li>안녕하세요. 게스트님</li>
      <li><a href="/cart">장바구니</a></li>
    </ul>
  </nav>
</header>

<article class="product">
  <div class="product-main">
    <div class="image-container">
      <div class="slider">
<img class="slider-item left" src="{product.images[sliderLeftIndex]}" alt="{product.name} 표지" />
<img class="slider-item" src="{product.images[sliderCenterIndex]}" alt="{product.name} 표지" />
<img class="slider-item right" src="{product.images[sliderRightIndex]}" alt="{product.name} 표지" />
<button class="slider-left-button" on:click={sliderMoveLeft}>이전</button>
<button class="slider-right-button"  on:click={sliderMoveRight}>다음</button>
        <!-- <img
        src="https://github.com/developer-book/svelte/blob/main/static/svelte-book-1.png?raw=true"
        alt="{product.name} 표지"
      /> -->

      </div>
      
    </div>
    <div>
      <h2>{product.name} </h2>
      <dl>
        <dt>금액</dt>
        <dd>{product.price} 원</dd>
      </dl>
      <div>
        {#if !cart.includes('svelte-book')}
          <button on:click={() => addToCart('svelte-book')}>장바구니 담기</button>
        {:else}
          <button disabled>장바구니 담기 완료</button>

        {/if}
    
      </div>
    </div>
    
    
  </div>
</article>

<footer>

  <h3>관련상품</h3>
  <ul>
    {#each releatedProducts as product}
      <li>
        <a href={`/product/${product.id}`}>{product.name} - {product.price}원</a>
      </li>
    {/each}

  </ul>

</footer>

<style>
  :global(body) {
    /* font-family: 'Avenir', sans-serif; */
    /* margin: 0; */
    /* padding: 0; */
    /* background-color: #f9f9f9; */
    margin: 0;
    background-color: #eee;
    padding: 0;
  }

  .header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 auto;
    background-color: #fff;
    padding: 0 15px;
    width: 100%;
    max-width: 800px;
    height: 50px;
  }

  .header-title {
    font-size: 1.5em;
    font-weight: bold;
    color: #333;
    text-decoration: none;
  }

  .header-links {
    display: flex;
    gap: 10px;
    margin: 0;
    list-style: none;
    padding: 0;
  }

  .product {
    margin: 0 auto;
    background-color: #fff;
    padding: 15px;
    width: 100%;
    max-width: 800px;
  }

  .product-main {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  .image-container {
    width: 100%;
    max-width: 400px;
    overflow: hidden;
  }

  .image-container img {
    width: 100%;
  }

  .slider {
   
   
    position: relative;
   width: 80%;
   margin: 0 10%;
  }

  .slider-item {
    /* position: absolute; */
    width: 100%;
    /* transition: transform 0.5s; */
  }

  .slider-item.left {
    /* transform: translateX(-100%); */
    position: absolute;
    top: 0;
    right: 100%;
  }

  .slider-item.right {
    /* transform: translateX(-100%); */
    position: absolute;
    top: 0;
    right: 100%;
  }

  .slider-left-button {
    position: absolute;
    top: 50%;
    right: 100%;
    
  }
  .slider-right-button {
    position: absolute;
    top: 50%;
    left: 100%;
    
  }

  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
