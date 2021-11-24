<script>
    import {fade} from "svelte/transition"

    let number = 0
    let show = false
    let src = 'https://www.lyon-ortho-clinic.com/files/cto_layout/img/placeholder/book.jpg'
    let alt = 'This is a Testing image'
    let value_array = []
    let list_value = ''

    function add_list() {
        if (list_value.trim().length > 0) {
            value_array = [...value_array, list_value]
            console.log(value_array)
        } else {
            alert('fill_The_Value')
        }
    }

    function
    incrementNumber() {
        if (show) {
            number += 1
        }
    }

    function decrementNumber() {
        if (show) {
            number -= 1
        }
    }

    function clear() {
        number = 0
    }

    // deleting some thing //
    function del_f() {
        value_array = value_array.slice(1)
    }

    function del_e() {
        value_array = value_array.slice(0, -1)
    }

    // delete By Click
    function remove(index) {
        value_array = value_array.filter((el, i) => {
            return i !== index;
        });
        console.log(value_array)
    }
</script>
<div class="container text-center">
    <div class="row">
        <div class="col-lg-5 m-auto">
            <div class="card">
                {#if show}
                    <div class="card-head"
                         transition:fade="{{delay: 250, duration: 1000}}"
                         class:colour={number>5}>{number > 0 ? number : 0}</div>
                {/if}
                <div class=" card-body">
                    <button class="btn btn-info mx-2" on:click={incrementNumber}>Increment</button>
                    <button class="btn btn-warning mx-2" on:click={decrementNumber}>Decrement</button>
                    <button class="btn btn-danger mx-2" on:click={clear}>Clear</button>
                    <button class="btn btn-primary mx-2" on:click={()=>show=!show}>{show ? 'Hide' : 'Show'}</button>
                    <div class="form-group">
                        <input type="text" class="form-control mt-5" bind:value={src}>
                    </div>
                    <img {src} {alt}/>
                    <form on:submit|preventDefault={add_list}>
                        <div class="form-group">
                            <input type="text" class="form-control mt-5" bind:value={list_value}>
                        </div>
                        <button class="btn btn-info my-2 " type="submit">Add</button>
                    </form>
                    <button class="btn btn-info my-2" on:click={del_f}>del_f</button>
                    <button class="btn btn-info my-2" on:click={del_e}>del_e</button>
                    {#each value_array as v,i (Date.now() + Math.floor(Math.random() * 1000))}
                        <p on:click={remove.bind(this,i)}>#{i + 1}</p>
                        <div class="alert alert-primary">{v}</div>
                    {:else }
                        <p>Please Add Something</p>
                    {/each}

                </div>
            </div>
        </div>
    </div>

</div>
<style>
    .card-head {
        background: #e0d6d6;
        padding: 20px 15px;
        font-weight: bold;
        border-radius: 5px;
    }

    .card {
        border: 3px solid #666666;
        border-radius: 5px;
        min-height: 300px;
        font-size: 30px;

    }

    .colour {
        color: purple;
        font-weight: 900;
        font-size: 40px;
    }

    img {
        height: 150px;
        width: 150px;
        margin-top: 10px;
        object-fit: cover;
    }
</style>