<template>
  <div class="commentaires">
    <h3>Commentaires</h3>
    <div
      v-for="commentaire in commentaires"
      :key="commentaire.id"
      class="display-commentaires"
    >
      <DisplayOneCommentaire :commentaire="commentaire" />
    </div>
  </div>
</template>

<script>
import CommentaireDataService from "../services/CommentaireDataService";
import DisplayOneCommentaire from "@/components/DisplayOneCommentaire.vue";

export default {
  name: "display-commentaire",
  props: ["posteId"],
  components: {
    DisplayOneCommentaire,
  },
  data() {
    return {
      commentaires: [],
    };
  },
  methods: {
    retrieveCommentaires() {
      CommentaireDataService.getAllCommentaires()
        .then((response) => {
          this.commentaires = response.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  beforeMount() {
    CommentaireDataService.getCommentairesByPoste(this.posteId)
      .then((response) => {
        this.commentaires = response.data;
        console.log(response.data);
      })
      .catch((e) => {
        console.log(e);
      });
    //this.retrieveCommentaires();
  },
};
</script>

<style lang="scss" scoped>
@import "../../variables.scss";

.commentaires {
  clear: both;
  &--unique {
    border-top: solid 2px $color-primary;
    border-bottom: solid 2px $color-primary;
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    align-items: center;
    flex-grow: 2;
  }
}
.icones {
  display: flex;
}
.commentaires {
  &--poste {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    margin-top: 1em;
    margin-bottom: 1em;
    &--titre {
      font-style: italic;
      margin: 0;
      span {
        color: $color-secondary;
      }
    }
    &--texte {
      margin: 0;
    }
  }
  &--delete {
    margin: 0.5em;
    padding: 0.5em 0.7em;
    border: 1px solid $color-secondary;
    border-radius: 10px;
    background: $color-secondary-lighter;
    cursor: pointer;
    height: 20%;
    &:hover {
      background: $color-secondary-light;
    }
    .fas {
      font-size: 1.2em;
      color: $color-secondary;
    }
  }
}
.commentaires {
  &--ajouter {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-between;
    align-items: center;
    input {
      flex-grow: 2;
      min-width: 0;
      padding: 0 1em;
      border: 1px solid $color-primary;
      height: 3rem;
      border-top-left-radius: 10px;
      border-bottom-left-radius: 10px;
    }
    button {
      background: $color-primary-lighter;
      border: 1px solid $color-primary;
      border-left: none;
      height: 3.13rem;
      font-size: 1em;
      color: $color-ajouter-commentaire;
      border-top-right-radius: 10px;
      border-bottom-right-radius: 10px;
      cursor: pointer;
      margin-right: 0.5rem;
      &:hover {
        background: $color-primary-light;
      }
    }
  }
}
.hidden {
  display: none;
}
</style>