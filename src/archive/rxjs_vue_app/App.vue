<template>
  <section class="section">
    <b-tabs v-model="activeTab">
      <b-tab-item v-for="person of people$" :key="person.id"
        :label="person.name"></b-tab-item>
    </b-tabs>
    <h1 class="title">{{ name$ }}</h1>
    <img v-stream:error="imageError$" :src="image$"/>
  </section>
</template>

<script>
import { from, combineLatest, merge } from 'rxjs'
import { pluck, map, switchMap, catchError, share, mapTo } from 'rxjs/operators'

export default {
  data () {
    return {
      activeTab: 0
    }
  },
  domStreams: ['click$', 'imageError$'],
  name: 'app',
  subscriptions () {
    const createLoader = url => from(this.$http.get(url)).pipe(pluck('data'))

    const cache = {}
    const cachePerson = cache => url =>{
      return cache[url] ? cache[url] : (cache[url] = createLoader(url))
    }

    const people$ = createLoader(`https://starwars.egghead.training/people`)

    const activeTab$ = this.$watchAsObservable('activeTab', { immediate: true }).pipe(
      pluck('newValue')
    )

    const person$ = combineLatest(activeTab$, people$, (tabId, people) => people[tabId].id
  ).pipe(map(id => `https://starwars.egghead.training/people/${id}`),
    switchMap(cachePerson(cache)), catchError(() => createLoader(`https://starwars.egghead.training/people/2`)),
    share())
    const name$ = person$.pipe(pluck('name'))
    const loadImage$ = person$.pipe(pluck('image'), map(image =>
      `https://starwars.egghead.training/${image}`))
    const failImage$ = this.imageError$.pipe(mapTo(`http://via.placeholder.com/400x400`))
    const image$ = merge(loadImage$, failImage$)
    return {
      people$,
      name$,
      image$
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
<!--
domStreams: ['click$', 'imageError$'],
name: 'app',
subscriptions () {
  const cache = {}
  const cachePerson = cache => url => {
    return cache[url] ? cache[url] : (cache[url] = createLoader(url))
  }

  const createLoader = url => from(this.$http.get(url)).pipe(pluck('data'))
  const people$ = createLoader(`https://starwars.egghead.training/people`).pipe(
    map(people => people.slice(0, 20)))

  const activeTab$ = this.$watchAsObservable('activeTab', { immediate: true }).pipe(pluck('newValue'))

  const luke$ = activeTab$.pipe(combineLatest(people$, (tabId, people) => people[tabId].id),
    map(id => `https://starwars.egghead.training/people/${id}`),
    switchMap(cachePerson(cache)), catchError(() => createLoader('https://starwars.egghead.training/people/2')),
    share())
  const disabled$ = merge(this.click$.pipe(mapTo(true)),
    luke$.pipe(mapTo(false))).pipe(startWith(false))
  const buttonText$ = disabled$.pipe(map(bool => bool ? 'Loading ...' : 'Load'))
  const name$ = luke$.pipe(pluck('name'))
  const loadImage$ = luke$.pipe(pluck('image'), map(image => `https://starwars.egghead.training/${image}`))
  const failImage$ = this.imageError$.pipe(mapTo(`http://via.placeholder.com/400x400`))
  const image$ = merge(loadImage$, failImage$)
  return {
    name$,
    image$,
    disabled$,
    buttonText$,
    activeTab$,
    people$
  }
}-->
