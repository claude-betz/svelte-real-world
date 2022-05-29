<svelte:head>
	<title>Conduit</title>
</svelte:head>

<script>
    import { page } from '$app/stores';
    $: tab = $page.url.searchParams.get('tab') || 'all';
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
								class:active={tab === 'all'}
							>
								Global Feed
							</a>
						</li>

                        <li class="nav-item">
                            <a href="/?tab=feed" rel="prefetch" class="nav-link" class:active={tab === 'feed'}>
                                Your Feed
                            </a>
                        </li>
                        <li class="nav-item">
                            <a href="/login" rel="prefetch" class="nav-link">Sign in to see your Feed </a>
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
					</div>
				</div>
			</div>
		</div>
	</div>
</div>