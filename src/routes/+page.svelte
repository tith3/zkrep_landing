<script lang=ts>
	import BetterInput from "$lib/components/BetterInput.svelte";
</script>

<div class="size-full bg-gradient-to-br variant-gradient-primary-secondary flex justify-center items-center py-4 px-4 sm:py-10 sm:px-16 md:px-28">
	<div class="card grow h-full rounded-lg flex flex-col py-12 sm:py-16 px-10 sm:px-20 sm:gap-4 gap-6 items-center sm:items-start">
		<div class="flex flex-row gap-2 w-full items-start">
			<img src="/images/zkrep.jpg" class="w-20 h-20 rounded-full"/>
			<h1 class="text-secondary-600 p-2 w-full text-4xl justify-center sm:justify-start my-auto font-semibold">zkReputation</h1>
		</div>
		<h2 class="text-2xl text-on-success-token">Unlock fair airdrops, secure credit, and compliant DeFi</h2>
		<p class="card card-hover w-full variant-ghost-success text-xl p-4 rounded-lg flex justify-center">Coming Soon!</p>
		<div class="w-full flex flex-row gap-4 h-full">
			<div class="flex flex-col gap-4 justify-between"  >
				<div class="flex flex-col grow size-full justify-center">
					<p class="text-5xl font-serif  justify-self-center ">GET NOTIFIED WHEN WE WILL LAUNCH!</p>
				</div>
				<div class="w-full flex flex-col gap-4 justify-end grow">
					<div class="w-full variant-ringed-secondary rounded-lg">
						<BetterInput placeholder="Enter your email" />
					</div>
					<button class="btn w-full rounded-lg variant-filled-secondary">SUBSCRIBE</button>
				</div>	
			</div>
			<img src="/images/businessman-excited-to-launch-new-project.svg" class="lg:block hidden"/>
		</div>
		

	</div>
</div>