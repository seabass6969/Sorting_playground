<script>
function gen_randnum(range){
    return Math.floor(Math.random()*range)
}
function gen_randlist_fromrange(range){
    let return_list = []
    for(let i=0; i<range; i++){
        return_list.push(gen_randnum(range))
    }
    return return_list
}
function regenerate(){
    list_random = gen_randlist_fromrange(100)
}
let sleepTime = 1
let list_random = gen_randlist_fromrange(100)
console.log("The arrays of it is: ")
console.log(list_random)
let on_sort_one = -1
let on_sort_two = -1
function sleep(delay) {
  return new Promise(resolve => setTimeout(resolve, delay));
}
let button_disable = false 
async function Bubble_sort(){
    button_disable = true 
    for(let i=0; i < (Math.floor(list_random.length) + 1); i++){
        for(let x=0; x<list_random.length;x++){
            on_sort_one = x
            on_sort_two = x+1
            // visual 
            if(!(x==(list_random.length - 1))){
                if(list_random[x] > list_random[x+1]){
                    let swap_a = list_random[x]
                    let swap_b = list_random[x+1]
                    list_random[x] = swap_b
                    list_random[x+1] = swap_a
                }
            }else{

            }
            await sleep(sleepTime)
        }
    }
    console.log("finish")
    on_sort_one = -1
    on_sort_two = -1
    button_disable = false
}
async function merge_sort(){
    button_disable = true
    for(let i=0; i<list_random.length;i++){
        let item = list_random[i]
        let y = i - 1;
        while(y >= 0 && list_random[y] > item){
            on_sort_one = y + 1
            on_sort_two = i
            list_random[y + 1] = list_random[y]
            y = y - 1
            await sleep(sleepTime)
        }
        list_random[y + 1] = item
    }
    console.log("finish")
    on_sort_one = -1
    on_sort_two = -1
    button_disable = false
}
</script>

<main>
    <div class="compactedsort">
        {#each list_random as index,i}
            {#if i==on_sort_one || i==on_sort_two}
                <div class="index" style="height: calc(80vh/100*{index}); margin-top: calc(80vh/100*{100-index}); background-color: red"></div>
            {:else}
                <div class="index" style="height: calc(80vh/100*{index}); margin-top: calc(80vh/100*{100-index}); background-color: purple"></div>
            {/if}
        {/each}
    </div>
    <div class="menu">
        <span>Sorting</span>
        <button on:click={regenerate} disabled="{button_disable}">rengenerate</button>
        <button on:click={()=> Bubble_sort()} disabled="{button_disable}">Bubble Sort</button>
        <button on:click={()=> merge_sort()} disabled="{button_disable}">merge Sort</button>
        <input type="number" name="delay" id="" bind:value={sleepTime}>
    </div>
</main>

<style>
.compactedsort{
    display: grid;
    grid-template-rows: auto;
    
}
.index{
    display: inline-grid;
    grid-row-start: 1;
    grid-row-end: 1;
    padding: 1px;
    width: 6px;
    background-color: purple;
}
.menu{
    margin-top: 10px
}
</style>
