<div class="card">
    <div class="title">
        <slot name ="title"></slot>
    </div>

    <div class="body">
        <slot></slot>
    </div>
</div>

<style>
    .card {
        border: 1px solid lightgray;
    }

    .title{
        border-bottom: 1px solid lightgray;
        padding: .5em 1em;
    }
    .body{
        padding: .5em 1em;
    }
</style>