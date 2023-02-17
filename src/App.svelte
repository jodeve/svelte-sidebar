<script>
	let links = [
		{
			name: "Home",
			icon: "home-outline"
		},
		{
			name: "Profile",
			icon: "person-outline"
		},
		{
			name: "Settings",
			icon: "settings-outline"
		},
		{
			name: "Logout",
			icon: "log-out-outline"
		}
	];
	let open = false;
	const onOpen = () => {
		open = !open;
	}
	let link = "Home";

	const onChangeLink = (linkName) => link = linkName;


	$: isActive = (linkName) => link == linkName ? 'active' : ''
</script>

<div class="body">
	<div class="sidebar" style="
		width: {open ? '260' : '70'}px; 
		align-items: {open ? 'start' : 'center'};
		padding: {open ? '10px' : '10px 5px 5px 5px'};
	">
		<div on:click="{onOpen}" class="button">
			{#if open}
				<ion-icon name="close-outline"></ion-icon>
			{:else}
				<ion-icon name="menu-outline"></ion-icon>
			{/if}
		</div>
		<div class="avatar">
			<img 
				class="rounded-circle" 
				src="/avatar.jpg" alt="avatar" 
				width="{open ? '100' : '40'}" 
				height="{open ? '100' : '40'}" 
			/>
		</div>
		<ul
			style="width: {open ? '100%' : ''}"
		>
			{#each links as link }
				<li class="nav-link-item {isActive(link.name)}" on:click="{ () => onChangeLink(link.name) }">
					<ion-icon name="{link.icon}"></ion-icon>
					{#if open}
						<span>{link.name}</span>
					{/if}
				</li>
			{/each}
		</ul>
	</div>
</div>

<style>
	.body{
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.sidebar{
		background-color: rgb(22, 22, 22);
		display: flex;
		flex-direction: column;
		box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
		border-radius: 2px;
		position: fixed;
		padding-top: 10px;
	}
	.button{
		border-radius: 50%;
		display: flex;
		font-size: 20px;
	}
	.button:hover{
		background-color: #f2f2f2;
		color: rgb(22, 22, 22);
	}
	.avatar{
		margin: 20px 0;
		width: 100%;
		text-align: center;
	}
	ul{
		padding: 0;
		list-style: none;
	}
	.nav-link-item{
		display: flex;
		align-items: center;
		padding: 5px;
		border-radius: 5px;
		cursor: pointer;
	}
	.nav-link-item:not(:first-child){
		margin-top: 10px;
	}
	.nav-link-item:hover,
	.nav-link-item.active{
		background-color: #d95858;
		color: #fff;
	}
	span{
		position: relative;
		margin-left: 20px;
	}
	ion-icon{
		font-size: 30px;
	}
</style>
