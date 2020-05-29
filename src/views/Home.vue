<template>
  <div class="home">
    <HeaderHome />

    <CarouselHome />

    <ProductHighlight />

    <TeamMember />

    <PartnerTeam />

    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import HeaderHome from "../components/HeaderHome";
import CarouselHome from "../components/CarouselHome";
import ProductHighlight from "../components/ProductHighlight";
import TeamMember from "../components/TeamMember";
import PartnerTeam from "../components/PartnerTeam";
import Footer from "../components/Footer";

export default {
  name: "Home",
  components: {
    HeaderHome,
    CarouselHome,
    ProductHighlight,
    TeamMember,
    PartnerTeam,
    Footer
  }
};
</script>

<style scoped>
</style>