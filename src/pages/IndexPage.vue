<template>
  <div>
    <div class="row bg-black justify-center text-center q-pa-md">
      <div class="col-12 text-left">
        <div
          :class="{
            classA: scrollPosition == 0,
            classB: scrollPosition > 0,
          }"
        >
          <div class="row">
            <div class="col-4 q-pl-md q-mt-md">
              <q-btn
                unelevated
                round
                color="grey-2"
                class="text-grey-9"
                icon="ios_share"
                @click="abrirDialog()"
              />
            </div>
            <div class="col-4 q-mt-md text-center">
              <div class="text-subtitle1 text-weight-bold">@opencod3</div>
            </div>
            <div class="col-4 q-mt-md q-pr-md text-right">
              <q-avatar size="44px">
                <img src="../assets/LOGO_OPENCOD3.png" />
              </q-avatar>
            </div>
          </div>
        </div>
      </div>
      <div class="col-6 text-left q-pl-md">
        <q-btn
          @click="abrirDialog()"
          unelevated
          round
          color="grey-2"
          class="text-grey-9"
          icon="ios_share"
        />
      </div>
      <div class="col-6"></div>
      <div class="col-12">
        <q-avatar size="96px">
          <img src="../assets/LOGO_OPENCOD3.png" />
        </q-avatar>
      </div>
      <div class="col-12 q-pt-md">
        <div class="text-subtitle1 text-grey-2 text-weight-bold">@opencod3</div>
      </div>
      <div class="col-12">
        <div class="text-caption text-grey-4 text-weight-mediumn">
          Você pode colocar aqui a sua descrição entre outros detalhes que achar
          interessante
        </div>
      </div>
      <div class="col-12 q-pt-xl">
        <div class="row">
          <div class="col-md-3 col-sm-12 col-xs-12"></div>
          <div class="col-md-6 col-sm-12 col-xs-12">
            <div class="q-py-sm" v-for="i in links" :key="i.id">
              <q-btn
                rounded
                unelevated
                color="grey-8"
                size="md"
                class="full-width q-py-md"
                @click="abrirLink(i)"
                :label="i.descricao"
              >
              </q-btn>
            </div>
          </div>
          <div class="col-md-3 col-sm-12 col-xs-12"></div>
        </div>
      </div>
    </div>
    <q-dialog v-model="dialog">
      <q-card id="borda" full-width>
        <q-card-section class="row">
          <div class="text-subtitle1 q-pl-xl text-center">
            Compartilhar Link
          </div>
          <q-space />
          <q-btn icon="close" size="sm" flat round dense v-close-popup />
        </q-card-section>
        <q-card-section>
          <q-list>
            <q-item
              @click="abrirLink(i)"
              id="borda"
              clickable
              v-ripple
              v-for="i in compartilhamentos"
              :key="i.id"
            >
              <q-item-section avatar>
                <q-icon :name="i.icone" />
              </q-item-section>
              <q-item-section>{{ i.descricao }}</q-item-section>
              <q-item-section avatar>
                <q-icon size="xs" name="chevron_right" />
              </q-item-section>
            </q-item>
          </q-list>
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import { openURL } from "quasar";
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  unmounted() {
    window.removeEventListener("scroll", this.updateScroll);
  },
  mounted() {
    window.addEventListener("scroll", this.updateScroll);
  },
  data() {
    return {
      scrollPosition: 0,
      dialog: false,
      compartilhamentos: [
        {
          id: 1,
          descricao: "Compartilhar via Whatsapp",
          icone: "img:whatsapp-56x56.webp",
          url: "https://wa.me/?text=Olha esse perfil de programação! - https://www.instagram.com/opencod3/?utm_source=linktree_profile_share&ltsid=5417ee14-229a-4156-b697-4eb1cc662abf",
        },
        {
          id: 2,
          descricao: "Compartilhar via Linkedin",
          icone: "img:linkedin.png",
          url: "https://www.linkedin.com/sharing/share-offsite/?url=https://www.instagram.com/opencod3/?utm_source=linktree_profile_share&ltsid=5417ee14-229a-4156-b697-4eb1cc662abf",
        },
        {
          id: 3,
          descricao: "Compartilhar via Facebook",
          icone: "img:facebook.png",
          url: "https://www.facebook.com/sharer.php?u=https://www.instagram.com/opencod3/?utm_source=linktree_profile_share&ltsid=5417ee14-229a-4156-b697-4eb1cc662abf",
        },
        {
          id: 4,
          descricao: "Compartilhar via Twitter",
          icone: "img:twitter.png",
          url: "https://twitter.com/intent/tweet?text=Olha esse perfil de programação! - https://www.instagram.com/opencod3/?utm_source=linktree_profile_share&ltsid=5417ee14-229a-4156-b697-4eb1cc662abf",
        },
      ],
      links: [
        {
          id: 1,
          url: "https://www.instagram.com/opencod3/",
          descricao: "GRUPO WHATSAPP",
        },
        {
          id: 2,
          url: "https://www.instagram.com/opencod3/",
          descricao: "VISITE O MEU SITE",
        },
        {
          id: 3,
          url: "https://www.instagram.com/opencod3/",
          descricao: "ENTRE NO MEU GRUPO DO TELEGRAM",
        },
        {
          id: 4,
          url: "https://www.instagram.com/opencod3/",
          descricao: "GRUPO WHATSAPP",
        },
        {
          id: 5,
          url: "https://www.instagram.com/opencod3/",
          descricao: "VISITE O MEU SITE",
        },
        {
          id: 6,
          url: "https://www.instagram.com/opencod3/",
          descricao: "ENTRE NO MEU GRUPO DO TELEGRAM",
        },
      ],
    };
  },
  methods: {
    abrirLink(link) {
      openURL(link.url);
    },
    abrirDialog() {
      this.dialog = !this.dialog;
    },
    updateScroll() {
      this.scrollPosition = window.scrollY;
    },
  },
});
</script>
<style lang="scss">
#borda {
  border-radius: 5px;
}
.q-btn--outline:before {
  border-color: #5861a0;
}
.classA {
  display: none;
}
.classB {
  transition: background-color 100ms ease 0s, -webkit-transform 100ms ease 0s,
    -webkit-backdrop-filter 100ms ease 0s;
  z-index: 10;
  width: calc(100% - 24px);
  position: fixed;
  border: 1px solid rgb(235, 238, 241);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 45px;
  height: 72px;
  backdrop-filter: blur(10px);
}
</style>
