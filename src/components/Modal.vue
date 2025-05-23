<template>
    <section class="modal">
        <div>
            <div @click="closeModal" class="closeModal cross">
                <div class="crossbar topBar"></div>
                <div class="crossbar bottomBar"></div>
            </div>
            <div class="modal-body">
                <div class="modal-text">
                    <div>
                        <p class="h3">{{project.title}}</p>
                        <p class="generalText orangeText">{{project.date}}</p>
                        <p class="generalText">{{project.description}}</p>
                        <p class="generalText">Made with: <span class="orangeText">{{project.development}}</span></p>
                    </div>
                </div>
                <div class="modal-image">
                    <img v-if="!project.isVideo" :src="'/images/projects/'+project.preview" :alt="'Preview of ' + project.title + 'webpage'">
                    <video v-else width="100%" height="auto" controls>
                        <source :src="'/images/projects/'+project.video" type="video/mp4">
                        Your browser does not support the video tag.
                    </video>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup lang="ts">
    import { defineEmits } from 'vue';
    const emits = defineEmits(['closeModal']); 

    defineProps({
        project: {
            type: Object,
            required: true,
        },
    });
    function closeModal() {
        emits('closeModal');
        return;
    }
</script>