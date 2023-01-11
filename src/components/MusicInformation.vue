<template>
  <div class="information-container">
    <div class="thumbnail-container">
      <img src="../assets/images/thumbnail.png" alt="A purple spiral" class="thumbnail"/>
    </div>
    <div class="information">
      <h1 class="title">
        Acorda Devinho
      </h1>
      <p class="author">
        Banda Rocketseat
      </p>
    </div>
  </div>
</template>

<style scoped>
.information-container {
  display: flex;
  flex-direction: column;
}

.thumbnail-container {
  width: 100%;
  height: 190px;
  border-radius: 6px;
  margin-bottom: 29px;
}

.thumbnail {
  width: 100%;
  height: 100%;
}

.information {
  display: flex;
  flex-direction: column;
}

.title, .author {
  color: var(--white);
}

.title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 10px;
}

.author {
  font-size: 1.2rem;
  font-weight: 400;
  opacity: 0.67;
}

@media (min-width: 48em) {
  .information-container {
    flex-direction: row;
  }

  .thumbnail-container {
    width: 84px;
    height: 84px;
    margin-bottom: 0;
    margin-right: 29px;
  }

  .information {
    justify-content: center;
  }
}
</style>
