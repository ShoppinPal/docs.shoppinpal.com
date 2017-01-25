# Better search with NGram

## Better Search? What does it mean, better how?

Let's say a user wants to search for: `gift ideas` in their notes but they accidently type `gist ideas`. One of the notes which should match as a search result has the title which contains `super cool gifts list` ... what now?

It means the search engine needs to be configured better and one way to do that is by using `nGram`.

1. A well configured `nGram` tool, would break the word `gifts` from the original title, down into various combinations such as:
```
gi | if | ft
gif | ift
gift
```
and store it for matching when a search occurs.

2. So even if users accidently used the word `gist` in their search, it would be broken down into:
```
gi | is | st
gis | ist
gist
```
and at least a partial match would exist between the many broken down tokens: `gi`

3. The same concept applies to full-text search (FTE) anywhere: websites, blogs, eCommerce or personal notes.

## Understanding NGram visually

NGram vs. Edge NGram — The NGram token filter generates all n-grams of the configured sizes for each token. For example, with the default settings (min_gram=1 and max_gram=2), “brown” is tokenized into:

`[b] [r] [o] [w] [n] [br] [ro] [ow] [wn]`

The Edge NGram token filter only generates n-grams from the beginning of the word:

`[b] [br]`

If you use edge n-grams, you will probably want to increase max_gram so you generate a few more terms. Setting it to 5 would yield:

`[b] [br] [bro] [brow] [brown]`

N-grams allow matching in the middle of words at the cost of more tokens and a larger index. If you’re not interested in matching in the middle of words and you want to save space, edge n-grams might be a better choice. For words like “brown”, it is unlikely that a user will search for “rown” (unless he makes a typo), and it is perhaps even undesirable that a search for “own” will match “brown”, so matching in the middle of words may not be important. On the other hand, your users may expect “ball” to match a compound word like “baseball”, in which case matching in the middle of words may be desirable.

The Edge NGram token filter can be configured to generate n-grams that include the end of the word instead of the beginning, although I’m not sure what the use case for this would be. Also, if you prefer tokenizers over token filters, there is an Edge variant of the NGram tokenizer called (you guessed it!) the Edge NGram tokenizer.

## Examples

Well tuned queries can be matched directly:

```
Query: j
Analyzed Query Terms: [j]
Document Terms: [ju] [um] [mp] [jum] [ump] [jump]
 
Query: ju
Analyzed Query Terms: <ju>
Document Terms: <ju> [um] [mp] [jum] [ump] [jump]
 
Query: jum
Analyzed Query Terms: <jum>
Document Terms: [ju] [um] [mp] <jum> [ump] [jump]
 
Query: jump
Analyzed Query Terms: <jump>
Document Terms: [ju] [um] [mp] [jum] [ump] <jump>
```

## Credit where credit is due - References

* [Control+R is Jon Tai's technical blog, powered by WordPress](https://jontai.me/blog/2013/02/adding-autocomplete-to-an-elasticsearch-search-application/)
    * A significant portion of this page comes from Jon Tai's blog. The blog was not heavily anchored so it became quite difficult to reference readers via `link & scroll` to the relevant content directly. Therefore, some content is repeated here for creative control of a reader's learning experience.
    * Blogs sometimes go down or disappear. It felt downright unethical to clone an article as HTML or PDF so instead here is a [scrolling screen capture](https://www.dropbox.com/s/hnf3s2kjsnp0lov/Adding%20Autocomplete%20to%20an%20elasticsearch%20Search%20Application.png?dl=0) via SnagIt. Hoping that this can fall in the "ok as a backup for readers" non-infringing zone.
