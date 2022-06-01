export const dnd = () => {
  return await useFetch(() => `https://www.dnd5eapi.co/api/${queryString.value}`, { pick: ['results'] } )
}