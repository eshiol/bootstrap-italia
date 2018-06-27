---
layout: docs
title: Tooltip
description: Documentazione ed esempi per aggiungere tooltips personalizzati di Bootstrap con CSS e JavaScript utilizzando CSS3 per animazioni e attributi data per l'archiviazione di titoli locali.
group: componenti
toc: true
---

{% capture callout %}
##### Accessibiltà: I tooltip funzionano sia con la tastiera che per gli utenti dotati di tecnologia assistiva

È importante aggiungere tooltip solo ad elementi HTML che sono tradizionalmente attivabili da tastiera e interattivi (link,
bottoni, o elementi di form).

Sebbene arbitrariamente gli elementi HTML (come `<span>`) possano essere resi attivabili tramite l'attributo `tabindex="0"`,
ciò aggiungerà interruzioni di tabulazioni potenzialmente dannose per gli utenti che usano la tastiera per navigare.
Inoltre, la maggior parte delle tecnologie assistive in questa situazione non annuncia il tooltip come ci si potrebbe
invece attendere.

Infine, non fare affidamento esclusivamente sull'`hover` come innesco del tooltip, in quanto ciò renderà impossibile
l'attivazione per gli utenti che usano la tastiera per navigare.
{% endcapture %}{% include callout.html content=callout type="accessibility" %}

Cose da sapere quando usi il plugin tooltip:

- I tooltip si basano sulla libreria di terze parti [Popper.js](https://popper.js.org/).
Per fare in modo che i tooltip funzionino è quindi necessario includere `popper.min.js` prima di
bootstrap-italia.js o usare la versione _bundle_ che contiene già Popper.js.
- I tooltip sono opt-in per ragioni di performance, quindi **devi inizializzarli tu stesso** con il codice che trovi di seguito.
- I tooltip con titoli vuoti non saranno mai visualizzati.
- Specifica `container: 'body'` per evitare problemi di rendering in componenti più complessi (come nei gruppi di input, gruppi di bottoni, etc).
- Attivare i tooltip su elementi nascosti non funzionerà.
- I tooltip per gli elementi `.disabled` o `disabled` devono essere attivati da un elemento contenitore.
- Quando attivati da collegamenti ipertestuali che si estendono su più righe, i tooltip verranno centrati. Usa `white-space: nowrap;`sui tuoi `<a>` per evitare questo comportamento.
- I tooltip devono essere nascosti prima che i loro elementi corrispondenti siano stati rimossi dal DOM.

## Esempio: Abilita i tooltip ovunque

Un modo per inizializzare tutti i tooltip su una pagina è quello di selezionarli tramite il loro attributo `data-toggle`:

{% highlight js %}
$(function () {
  $('[data-toggle="tooltip"]').tooltip()
})
{% endhighlight %}

## Esempi

Passa il mouse sopra i link sottostanti per visualizzare i tooltip:

<div class="bd-example tooltip-demo">
  <p class="muted">
    Ecco un <a href="#" data-toggle="tooltip" title="Primo tooltip">bianco scenario</a><br/>
    per tratteggiarvi l’accompagnamento<br/>
    degli oggetti di sfondo che pur vivono.<br/>
    Non ne sarò <a href="#" data-toggle="tooltip" title="Secondo tooltip">l’artefice</a> impaziente.<br/>
    Berrò alle coppe della nostalgia,<br/>
    avrò preteso d’ozio nelle lacrime...<br/>
    perché non mi ribello alla natura:<br/>
    la mia lentezza li esaspera...<br/>
    La mia lentezza? No, la mia fiducia.<br/>
    Per adesso è deserto.<br/>
    <a href="#" data-toggle="tooltip" title="Terzo tooltip">Il mondo può rifarsi senza me</a>,<br/>
    E intanto gli altri mi denigreranno
  </p>
  <p>
    <em>La città nuova, Alda Merini</em>
  </p>
</div>

Passa il mouse sopra i bottoni sottostanti per vedere le quattro direzioni dei tooltip: sopra, destra, sotto, e sinistra.

<div class="bd-example tooltip-demo">
  <div class="bd-example-tooltips">
    <button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="top" title="Tooltip on top">Tooltip in alto</button>
    <button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="right" title="Tooltip on right">Tooltip a destra</button>
    <button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="bottom" title="Tooltip on bottom">Tooltip in basso</button>
    <button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="left" title="Tooltip on left">Tooltip a sinistra</button>
    <button type="button" class="btn btn-secondary" data-toggle="tooltip" data-html="true" title="<em>Tooltip</em> <u>with</u> <b>HTML</b>">Tooltip con HTML</button>
  </div>
</div>

{% highlight html %}
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="top" title="Tooltip on top">
  Tooltip in alto
</button>
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="right" title="Tooltip on right">
  Tooltip a destra
</button>
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="bottom" title="Tooltip on bottom">
  Tooltip in basso
</button>
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-placement="left" title="Tooltip on left">
  Tooltip a sinistra
</button>
{% endhighlight %}

E con codice HTML personalizzato:

{% highlight html %}
<button type="button" class="btn btn-secondary" data-toggle="tooltip" data-html="true" title="<em>Tooltip</em> <u>with</u> <b>HTML</b>">
  Tooltip con HTML
</button>
{% endhighlight %}

## Uso

Il plugin del tooltip genera contenuto e markup su richiesta, e in modo predefinito posiziona i tooltip dopo i loro elementi attivati.

Attivare il tooltip tramite JavaScript:

{% highlight js %}
$('#example').tooltip(options)
{% endhighlight %}

### Markup

Di seguito è mostrato un esempio che esplicita il funzionamento interno di Bootstrap per la gestione di Tooltip.

Il markup richiesto per un tooltip è costituito da un attributo `data-` e `title` sull'elemento HTML sul quale si vuole
abilitare un tooltip. Ad esempio, quando nella pagina è scritto questo codice HTML:

{% highlight html %}
<a href="#" data-toggle="tooltip" title="Testo di esempio del tooltip">Link che attiva il tooltip</a>
{% endhighlight %}

Nel momento in cui tale elemento riceve focus da tastiera (o c'è un evento `hover`), Bootstrap genera il markup seguente:

{% highlight html %}
<a href="#" data-toggle="tooltip" title="Testo di esempio del tooltip!" aria-describedby="tooltip0123456">Link che attiva il tooltip</a>

<div class="tooltip bs-tooltip-top" role="tooltip" id="tooltip0123456">
  <div class="arrow"></div>
  <div class="tooltip-inner">Testo di esempio del tooltip</div>
</div>
{% endhighlight %}

### Opzioni

Le opzioni possono essere passate tramite attibuti data o tramite JavaScript. Per gli attributi data, aggiungi l'opzione nome a `data-`, come in `data-animation=""`.

Per ulteriori informazioni si rimanda alla sezione [tooltip](https://getbootstrap.com/docs/4.1/components/tooltips/) del sito di Bootstrap.

### Metodi

{% include callout-danger-async-methods.md %}

#### `$().tooltip(options)`

Allega un gestore del tooltip a una raccolta di elementi.

#### `.tooltip('show')`

Mostra il tootlip di un elemento. **Ritorna al chiamante prima che il tooltip sia stato effettivamente mostrato** (i.e. prima che si verifichi l'evento `shown.bs.tooltip`). Questo è considerato un'attivazione "manuale" del tooltip. I tooltip senza titoli non vengono mai visualizzati.

{% highlight js %}$('#element').tooltip('show'){% endhighlight %}

#### `.tooltip('hide')`

Nascondi il tootltip di un elemento. **Ritorna al chiamante prima che il tooltip sia stato effettivamente nascosto** (i.e. prima che si verifichi l'evento `hidden.bs.tooltip`). Questo è considerato un'attivazione "manuale" del tooltip.

{% highlight js %}$('#element').tooltip('hide'){% endhighlight %}

#### `.tooltip('toggle')`

Attiva/Disattiva il tooltip di un elemento. **Ritorna al chiamante prima che il tooltip sia stato effettivamente mostrato o nascosto** (i.e. prima che si verifichi l'evento `shown.bs.tooltip` o l'evento `hidden.bs.tooltip`). Questo è considerato un'attivazione "manuale" del tooltip.

{% highlight js %}$('#element').tooltip('toggle'){% endhighlight %}

#### `.tooltip('dispose')`

Nasconde e distrugge il tooltip di un elemento.

{% highlight js %}$('#element').tooltip('dispose'){% endhighlight %}

#### `.tooltip('enable')`

Fornisce al tooltip di un elemento la possibilità di essere mostrato. **I tooltip sono abilitati in modo predefinito.**

{% highlight js %}$('#element').tooltip('enable'){% endhighlight %}

#### `.tooltip('disable')`

Rimuove la capacità di mostrare il tooltip di un elemento. Il tooltip potrà essere mostrato solo se è riattivato.

{% highlight js %}$('#element').tooltip('disable'){% endhighlight %}

#### `.tooltip('toggleEnabled')`

Attiva/disattiva la possibilità che il tooltip di un elemento sia mostrato o nascosto.

{% highlight js %}$('#element').tooltip('toggleEnabled'){% endhighlight %}

#### `.tooltip('update')`

Aggiorna la posizione del tooltip di un elemento.

{% highlight js %}$('#element').tooltip('update'){% endhighlight %}

### Eventi

<table class="table table-bordered table-striped">
  <thead>
    <tr>
      <th style="width: 150px;">Tipo di evento</th>
      <th>Descrizione</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>show.bs.tooltip</td>
      <td>Questo evento si attiva immediatamente quando viene chiamato il metodo <code>show</code>.</td>.
    </tr>
    <tr>
      <td>shown.bs.tooltip</td>
      <td>Questo evento viene attivato quando il tooltip è stato reso visibile all'utente (attenderà il completamento delle transizioni CSS).</td>
    </tr>
    <tr>
      <td>hide.bs.tooltip</td>
      <td>Questo evento si attiva immediatamente quando viene chiamato il metodo <code>hide</code>.</td>
    </tr>
    <tr>
      <td>hidden.bs.tooltip</td>
      <td>Questo evento viene generato quando il tooltip ha finito di essere nascosto all'utente (attenderà il completamento delle transizioni CSS).</td>
    </tr>
    <tr>
      <td>inserted.bs.tooltip</td>
      <td>Questo evento si attiva dopo l'evento <code>show.bs.tooltip</code> quando il modello del tooltip è stato aggiunto al DOM.</td>
    </tr>
  </tbody>
</table>

{% highlight js %}
$('#myTooltip').on('hidden.bs.tooltip', function () {
  // fai qualcosa
})
{% endhighlight %}