```sh
#!/usr/bin/env bash
set -e

echo "=== GitHub Pages Hard Bootstrap ==="

read -p "GitHub username: " GH_USER
read -p "Repository name: " GH_REPO
read -s -p "GitHub Personal Access Token: " GH_TOKEN
echo

API="https://api.github.com"
REPO_API="$API/repos/$GH_USER/$GH_REPO"

# ---- create repo if missing ----
curl -s -o /dev/null -w "%{http_code}" \
  -H "Authorization: token $GH_TOKEN" \
  "$REPO_API" | grep -q 200 || \
curl -s -X POST "$API/user/repos" \
  -H "Authorization: token $GH_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  -d "{
    \"name\": \"$GH_REPO\",
    \"private\": false,
    \"auto_init\": false
  }" >/dev/null

# ---- local setup ----
mkdir -p "$GH_REPO"
cd "$GH_REPO"

git init
git checkout -B ukhona

# ---- content ----
cat <<EOF > index.md
# GitHub Pages is live

Bootstrap successful.

EOF

git add index.md
git commit -m "bootstrap gh-pages"

# ---- remote ----
git remote remove origin 2>/dev/null || true
git remote add origin "https://$GH_USER:$GH_TOKEN@github.com/$GH_USER/$GH_REPO.git"

# ---- FORCE ALIGN (intentional) ----
git push -f origin ukhona

# ---- enable Pages ----
curl -s -X POST "$REPO_API/pages" \
  -H "Authorization: token $GH_TOKEN" \
  -H "Accept: application/vnd.github+json" \
  -d '{
    "source": { "branch": "ukhona", "path": "/" }
  }' >/dev/null || true

echo
echo "======================================"
echo "LIVE (may take ~30s):"
echo "https://$GH_USER.github.io/$GH_REPO/"
echo "======================================"
```

Exactly. Once you swallow “probabilistic all the way down,” an enormous amount of intellectual furniture suddenly snaps into alignment—with a click that’s [oddly satisfying](https://ukb-dt.github.io/ukb-bge-00/) and mildly unsettling.

Quantum mechanics is the cleanest statement of this worldview. Not “we don’t know yet,” but *the universe itself does not commit until interaction*. The wavefunction isn’t hiding certainty behind a curtain; it **is** uncertainty with structure. Probability isn’t epistemic embarrassment. It’s ontological plumbing.

[Cancer-as-bad-luck](https://ukb-dt.github.io/vogelstein/) sits squarely in the same basin. The ~67% figure isn’t nihilism; it’s a reminder that biological systems are stochastic reactors running for decades under thermal noise, cosmic rays, replication errors, and selection pressures that care only about [population-level adequacy](https://ukb-dt.github.io/invariance/), not individual fairness. Mutation is not a moral failure. It’s the cost of doing business in a universe that allows complexity at all.

Sapolsky’s *Determined* lands here too, though he leans harder than necessary. If every causal chain is probabilistic, then determinism becomes a statistical claim, not a Laplacian fantasy. You don’t get free will smuggled in—but you also don’t get the tyranny of inevitability. You get **constraint without script**. Outcomes are bounded, not prewritten.

This is where Prigogine is the missing keystone. He shows that irreversibility isn’t a bug layered on top of physics; it’s what happens when probabilistic systems are driven far from equilibrium. Time’s arrow emerges not from certainty, but from *amplified fluctuation*. Order doesn’t defeat randomness—it *rides* it.

Put these together and a pattern emerges:

Quantum mechanics gives you indeterminacy at the base.      
Biology turns that indeterminacy into variation.     
Evolution filters variation without foresight.     
Neuroscience inherits constrained stochasticity.     
Agency becomes attractor dynamics, not authorship.     
History becomes path-dependent, not scripted.      

Nothing here requires mysticism. Nothing here allows naïve control. And nothing here reduces life to clockwork. That’s why McGilchrist’s moralized hemispheres feel so out of place—they’re trying to reinsert intention where probability already does the explanatory work more honestly.

The universe you’re describing isn’t cold. It’s *generative*. It produces novelty because it cannot lock itself into certainty. Meaning doesn’t float above this system; it condenses locally, temporarily, the way vortices form in turbulent flow.

That’s Prigogine’s gift: showing that fragility is not failure. It’s the precondition for emergence.

And once you see that, “bad luck,” “no free will,” and “indeterminacy” stop sounding like insults. They start sounding like the price of being able to exist at all.

