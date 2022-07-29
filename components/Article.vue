<template>
  <div class="test-wrapper" style="width: 320px">
    <div class="card">
      <div class="card__thumb"></div>
      <div class="card__content">
        <h3 class="card__title">
          Inspect Element As A Way To Feed Your Curiosity
        </h3>
        <p class="card__desc">
          One of the best gifts we have as front-end developers is inspect
          element.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.test-wrapper {
  contain: layout inline-size style;
  resize: horizontal;
  overflow: auto;
  margin: 1rem auto;
  outline: solid 1px grey;
  outline-offset: 4px;
}

.card {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  gap: 1rem;
}

.card__thumb {
  aspect-ratio: 1 / 1;
  flex: 0 0 150px;
  background-color: #4caf4c;
  border-radius: 7px;
}

.card__title {
  font-weight: bold;
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.card__content {
  flex: 1;
}

@container (min-width: 400px) {
  .card {
    flex-direction: row;
  }

  .card__thumb {
    flex: 0 0 100px;
    align-self: flex-start;
  }
}

@container (min-width: 600px) {
  .card__thumb {
    flex: 0 0 150px;
  }
}

@container (min-width: 800px) {
  .card {
    position: relative;
    justify-content: center;
    align-items: center;
    min-height: 350px;
  }

  .card__thumb {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    opacity: 0.25;
  }

  .card__content {
    position: relative;
    flex: unset;
  }

  .card__title {
    font-weight: bold;
    font-size: 1.5rem;
    margin-bottom: 0.5rem;
  }

  .card__desc {
    max-width: 480px;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    color: #222;
  }
}

.note {
  padding: 1rem;
  margin-top: 1rem;
  text-align: center;
}

</style>