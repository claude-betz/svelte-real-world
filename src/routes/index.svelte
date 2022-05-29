<svelte:head>
	<title>Conduit</title>
</svelte:head>

<script context="module">
    export async function load({ url, fetch }) {
        const [{ articles, pages }, { tags }] = await Promise.all([
            fetch(`/articles.json${url.search}`, { credentials: 'include' }).then((r) => r.json()),
            fetch('/tags.json').then((r) => r.json())
        ]);

        return {
            props: {
                articles,
                pages,
                tags
            }
        };
    }
</script>

<script>
    import { page } from '$app/stores';
    $: tag = $page.url.searchParams.get('tag');
    $: tab = $page.url.searchParams.get('tab') || 'all';

    export let articles;
	export let pages;
	export let tags;
</script>


<div class="home-page">
    <div class="banner">
        <div class="container">
            <h1 class="logo-font">conduit</h1>
            <p>A place to share your knowledge.</p>
        </div>
    </div>

	<div class="container page">
		<div class="row">
			<div class="col-md-9">
				<div class="feed-toggle">
					<ul class="nav nav-pills outline-active">
						<li class="nav-item">
							<a
								href="/?tab=all"
								rel="prefetch"
								class="nav-link"
								class:active={tab === 'all' && !tag}
							>
								Global Feed
							</a>
						</li>

                        <li class="nav-item">
                            <a
                                href="/?tab=feed"
                                rel="prefetch"
                                class="nav-link"
                                class:active={tab === 'feed'}
                            >
                                Your Feed
                            </a>
                        </li>

                        <li class="nav-item">
                            <a
                                href="/login"
                                rel="prefetch"
                                class="nav-link"
                            >
                                Sign in to see your Feed
                            </a>
                        </li>

                        <li class="nav-item">
                            
                        </li>
					</ul>
				</div>
			</div>

			<div class="col-md-3">
				<div class="sidebar">
					<p>Popular Tags</p>
					<div class="tag-list">
						{#each tags as tag}
							<a href="/?tag={tag}" rel="prefetch" class="tag-default tag-pill"> {tag} </a>
						{/each}
					</div>
				</div>
			</div>
		</div>
	</div>
</div>