<template>
    <ion-card>
        <img alt="Silhouette of mountains" :src="item.image" />
        <ion-card-header>
            <ion-card-title>{{ item.name }}</ion-card-title>
            <ion-card-subtitle>{{ item.price }}</ion-card-subtitle>
        </ion-card-header>

        <ion-card-content>
            {{item.desc}}
        </ion-card-content>

        <ion-button @click="addToCart()">Add To Cart</ion-button>
        <ion-button @click="removeFromCart()">Remove From Cart</ion-button>
    </ion-card>
</template>
  
<script>
import { defineComponent, ref, onMounted } from 'vue';
//import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
//import ExploreContainer from '@/components/ExploreContainer.vue';
import { useRoute } from 'vue-router';

export default defineComponent({
    name: 'ItemPage',
    //components: { ExploreContainer, IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
    setup() {
        const item = ref({});
        const route = useRoute();
        const { id } = route.params;

        onMounted(async () => {

            var response = await fetch("https://api.npoint.io/5529943ab6c290922ca9");

            if (response.ok) {
                let fashionItems = await response.json();

                item.value = fashionItems.filter((item) => {
                    return item.id == id;
                })[0];
            }
        });

        return {
            item
        }
    }
});
</script>
  