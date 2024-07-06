<script lang=ts>
	import BetterInput from "$lib/components/BetterInput.svelte";
	import { getModalStore, type ModalSettings } from '@skeletonlabs/skeleton';


	const modalStore = getModalStore();
	
	let email = "";
	let emailError = "";

	function handleSetEmail() {
        //validate that email isn't empty
        if (email.trim() === "") {
            emailError = "Required"
            return;
        }
        //validate that email is valid
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email)) {
            emailError = "Invalid email format"
            return;
        }
        emailError=""
		//subscribe to email list
		new Promise<boolean>((resolve) => {
			const modal:ModalSettings = {
				type: "alert",
				title: 'Uh Oh!',
				body: 'This is just a demo page, the real zkReputation pre-launch page is https://zkrep.xyz/ . You will be redirected after pressing close.',
				response: (r: boolean) => {
					resolve(r);
				}
			};
			modalStore.trigger(modal);
		}).then((r: any) => {
			
			console.log("redirecting", r);
			window.location.href = "https://zkrep.xyz/";
		});
    }

</script>

<div class="size-full bg-gradient-to-br variant-gradient-primary-secondary flex justify-center items-center py-2 px-4 sm:py-10 sm:px-16 md:px-28 ">
	<div class="!overflow-auto card grow h-full rounded-lg flex flex-col py-12 sm:py-16 px-10 sm:px-20 sm:gap-4 gap-6 items-center sm:items-start">
		<div class="flex flex-row gap-2 w-full items-start">
			<img src="/images/zkrep.jpg" class="sm:size-20 size-14 rounded-full"/>
			<h1 class="text-secondary-600 p-2 w-full text-4xl justify-center sm:justify-start my-auto font-semibold">zkReputation</h1>
		</div>
		<h2 class="text-2xl text-on-success-token">Unlock fair airdrops, secure credit, and compliant DeFi</h2>
		<p class="card card-hover w-full variant-ghost-success text-xl p-4 rounded-lg flex justify-center">Coming Soon!</p>
		<div class="w-full flex flex-row gap-4 h-full">
			<div class="flex flex-col gap-4 justify-between"  >
				<div class="flex flex-col grow size-full justify-center">
					<p class="sm:text-5xl text-4xl font-serif  justify-self-center ">GET NOTIFIED WHEN WE WILL LAUNCH!</p>
				</div>
				<div class="w-full flex flex-col gap-4 justify-end grow">
					<BetterInput placeholder="Enter your email" onEnter={handleSetEmail} errorText={emailError} bind:value={email}/>
					<button class="btn w-full rounded-lg variant-filled-secondary" on:click={handleSetEmail}>SUBSCRIBE</button>
				</div>	
			</div>
			<img src="/images/businessman-excited-to-launch-new-project.svg" class="lg:block hidden"/>
		</div>
		

	</div>
</div>