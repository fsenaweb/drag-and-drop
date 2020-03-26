<template>
    <div class="box">
        <draggable
                :list="tasks"
                :disabled="!enabled"
                class="list-group"
                ghost-class="ghost"
                @start="dragging = true"
                @end="dragging = false"
                group="box"
        >
            <transition-group type="transition" :name="!dragging ? 'flip-list' : null">
                <div
                        class="list-group-item"
                        v-for="element in tasks"
                        :key="element.id"
                >
                    <div class="category"
                         :style="{ backgroundColor: element.category }"
                    />
                    <div class="content">
                        <div class="title">
                            {{ element.title }}
                        </div>
                        <div class="user">
                            <div v-for="(user, index) in element.users" :key="index">
                                <img :src="require('./../assets/images/' + user)" :alt="user">
                            </div>
                        </div>
                        <div class="status">
                            <div
                                    v-for="(color, index) in element.color"
                                    :key="index"
                                    :style="{
                                            width: '30px',
                                            height: '10px',
                                            borderRadius: '5px',
                                            marginLeft: '5px',
                                            backgroundColor: color
                                        }"
                            />
                        </div>
                    </div>
                </div>
            </transition-group>
        </draggable>
    </div>
</template>

<script>
    import draggable from "vuedraggable";

    export default {
        name: "Box",
        components: {
            draggable
        },
        data() {
            return {
                enabled: true,
                dragging: false,
                item: [
                    {
                        id: 100,
                        title: "Develop API",
                        category: 'green',
                        color: ['purple'],
                        users: ['user-3.jpg', 'user-1.jpg']
                    }
                ]
            };
        },
        props: {
            tasks: {
                type: Array,
                required: true
            }
        },
    };
</script>

<style>

    .flip-list-move {
        transition: transform .2s;
    }

    .no-move {
        transition: transform 0s;
    }

    .ghost {
        opacity: 0;
        background: #c8ebfb;
    }

    .list-group {
        width: 100%;
        min-height: 200px;
        box-sizing: border-box;
    }

    .list-group-item {
        max-width: 100%;
        height: 110px;
        box-sizing: border-box;
        background-color: #ffffff;
        margin: 10px 0;
        padding: 8px 8px 8px 12px;
        border-radius: 5px;
        cursor: move;
        display: flex;
        justify-content: flex-start;
        align-items: center;
    }

    .category {
        content: "";
        min-width: 8px;
        height: 60px;
        margin-left: -12px;
        margin-right: 17px;
        border-radius: 0 5px 5px 0;
    }

    .list-group-item i {
        cursor: pointer;
    }

    .title {
        font-size: 90%;
        margin: 8px 0;
    }

    .user {
        display: flex;
        flex-direction: row;
    }

    .user img {
        max-width: 35px;
        border-radius: 50%;
        margin-left: 5px;
    }

    .status {
        display: flex;
        flex-direction: row;
    }

</style>