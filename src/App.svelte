<script>
  // import Router from 'svelte-spa-router'
  // import { routes } from './routes'
  import Logo from './components/Logo.svelte'
  import Icon from './components/Icon.svelte'

  export let data = []
  let count = null
  async function getData() {
    await fetch(
      'https://api.datadesk.co.za/csvjson.php?table=dd_council_seats_583154'
    )
      .then((response) => response.json())
      .then((response) => {
        data = response.sort((a, b) =>
          a.Municipality > b.Municipality ? 1 : -1
        )

        let c = data.filter((d) => d.formed_council === 'yes')
        count = 70 - c.length
        // data.forEach((d) => {
        //   if (d.DA2021 == '') {
        //     d.DA2021 = 0
        //   }
        //   if (d.EFF2021 == '') {
        //     d.EFF2021 = 0
        //   }
        //   if (d.IFP2021 == '') {
        //     d.IFP2021 = 0
        //   }
        // })
      })
  }

  let promise = Promise.all([getData()])
</script>

<main>
  <div class="blurb top-blurb">
    <br />
    Sign our
    <a href="https://newsletter.theoutlier.co.za" target="_new">newsletter</a>
    for more data stories like this. Or follow us on
    <a href="https://twitter.com/outlierafrica" target="_new"
      ><Icon name="twitter" stroke="dodgerblue" strokeWidth="2" /></a
    >.
  </div>
  <Logo />
  <div class="blurb">
    <p>
      There were 70 hung municipalities following the 2021 local government
      elections at the start of November 2021. The deadline to constitute these
      councils was 23 November 2021. On 2&nbsp;December&nbsp;2021 the
      Modimolle-Mookgophong municipality in Limpopo, was the last to finalise a
      council by <a
        href="https://www.news24.com/news24/southafrica/news/heads-or-tails-r1-coin-toss-ensures-da-councillor-elected-mayor-in-limpopo-20211202"
        target="_blank">coin toss</a
      >.
    </p>
    <p>
      On the map below the councils that have not yet been finalised are in <span
        style="color: #D6604D;">red</span
      >
      and those that have are in <span style="color: #4393C3;">blue.</span>
    </p>
    <p>
      This table and map are <strong>updated automatically</strong> when new information
      becomes available.
    </p>
  </div>

  <div class="map">
    <iframe
      src="https://flo.uri.sh/visualisation/7951336/embed"
      title="Interactive or visual content"
      class="flourish-embed-iframe"
      frameborder="0"
      scrolling="no"
      sandbox="allow-same-origin allow-forms allow-scripts allow-downloads allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation"
    />
    <div
      style="width:100%!;margin-top:4px!important;text-align:right!important;"
    >
      <a
        class="flourish-credit"
        href="https://public.flourish.studio/visualisation/7951336/?utm_source=embed&utm_campaign=visualisation/7951336"
        target="_top"
        style="text-decoration:none!important"
        ><img
          alt="Made with Flourish"
          src="https://public.flourish.studio/resources/made_with_flourish.svg"
          style="width:105px!important;height:16px!important;border:none!important;margin:0!important;"
        />
      </a>
    </div>
  </div>

  <div class="table">
    <table>
      <tr><th>Municipality</th><th>Council Formed</th><th>Mayor</th></tr>
      {#each data as d}
        <tr
          ><td class="label"
            >{d.Municipality} <span class="light">({d.Province})</span>

            <div class="seats">
              <Icon name="user" stroke="black" strokeWidth="1" /> SEATS:<br />
              <span class="anc">ANC&nbsp;{d.ANC2021}</span> &nbsp;
              <span class="da">DA&nbsp;{d.DA2021}</span> &nbsp;
              <span class="eff">EFF&nbsp;{d.EFF2021}</span> &nbsp;
              <span class="ifp">IFP&nbsp;{d.IFP2021}</span> &nbsp;
              <span class="other">OTHERS&nbsp;{d.Others2021}</span>
            </div></td
          ><td
            class={d.formed_council === 'yes'
              ? 'confirmed status'
              : 'unconfirmed status'}
            >{d.formed_council}
          </td>
          <td class="mayor">{d.mayor_party}</td></tr
        >
      {/each}
    </table>
  </div>
  <div class="blurb">
    <br />
    Join our
    <a href="https://newsletter.theoutlier.co.za" target="_new">newsletter</a>
    for more like this. Or follow us on
    <a href="https://twitter.com/outlierafrica" target="_new"
      ><Icon name="twitter" stroke="dodgerblue" strokeWidth="2" /></a
    >.
  </div>
</main>

<style>
  main a {
    color: dodgerblue;
  }
  main {
    max-width: 600px;
    margin-bottom: 30px;
  }
  .confirmed {
    /* background: rgb(234, 247, 234); */
  }
  .unconfirmed {
    background: #bd3131;
    color: #fff;
  }
  table {
    border-collapse: collapse;
    font-family: var(--headerFont);
  }
  td {
    border: solid 3px #eee;
    background: #fff;
    padding: 10px;
  }
  th {
    border: solid 3px #eee;
    padding: 10px;
    background: #fff;
    background: #000;
    color: #fff;
  }
  .status {
    text-align: center;
    padding: 5px;
    text-transform: uppercase;
    font-size: 0.8rem;
  }
  .label {
    font-weight: 700;
    /* background: none; */
  }
  .seats {
    font-weight: 300;
    font-size: 0.7rem;
    line-height: 0.9rem;
    margin-top: 5px;
  }
  .anc {
    color: green;
  }
  .da {
    color: dodgerblue;
  }
  .eff {
    color: indianred;
  }
  .ifp {
    color: rgb(187, 153, 0);
  }
  .seats {
  }
  .blurb {
    text-align: center;
    font-size: 0.9rem;
  }
  .light {
    font-weight: 300;
  }
  .mayor {
    font-size: 0.8rem;
    text-transform: uppercase;
  }
  .top-blurb a {
    color: #000;
  }
  .top-blurb {
    border-bottom: solid 1px rgb(168, 168, 168);
    padding-bottom: 10px;
  }
  .flourish-embed-iframe {
    width: 100%;
    height: 500px;
  }

  @media only screen and (max-width: 600px) {
    .flourish-embed-iframe {
      height: 450px;
    }
  }
</style>
