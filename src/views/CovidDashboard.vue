<template>
  <div style="display: contents"> <!-- my wrapper div is rendered invisible -->

  <article id="work" class="wrapper style2">
  <div class="container">
    <header>
      <h2>Covid Statistics</h2>
      <p></p>
    </header>
    <div class="row aln-center">
      <div class="col-12">
        <section class="box style1">
          <h3>Worldwide Cases</h3>
          <p><iframe src="https://ourworldindata.org/grapher/total-cases-covid-19?tab=map" width="100%" height="600px" border="1px solid black"></iframe></p>
        </section>
      </div>
      <div class="col-12">
        <section class="box style1">
          <h3>Cumulative US Deaths</h3>
          <p><iframe src="https://ourworldindata.org/grapher/total-deaths-covid-19?country=USA" width="100%" height="600px" border="1px solid black"></iframe></p>
        </section>
      </div>
      <div class="col-12">
        <section class="box style1">
          <h3>North American Cases</h3>
          <p><iframe src="https://ourworldindata.org/grapher/covid-19-testing-policy" 
          width="100%" height="600px" border="1px solid black"></iframe></p>
        </section>
      </div>
    </div>
    <footer>
      <p>Data provided and updated daily by Our World in Data.</p>
    </footer>
  </div>
  </article>
  </div>
</template>
