<template>
  <composition :composition="composition">
    <Hero :uniformData="composition" />
    <slot-content slotName="innerHeroes" />
  </composition>
</template>

<script>
import {
  createContentfulEnhancer,
  CANVAS_CONTENTFUL_PARAMETER_TYPES
} from "@uniformdev/canvas-contentful";
import { enhance, EnhancerBuilder } from "@uniformdev/canvas";
import { createClient } from "contentful";

export default {
  async asyncData({ $uniformCanvasNuxt }) {
    const client = createClient({
      space: process.env.CONTENTFUL_SPACE_ID,
      environment: "master",
      accessToken: process.env.CONTENTFUL_DELIVERY_API_KEY
    });

    const { composition } = await $uniformCanvasNuxt.getCompositionBySlug({
      slug: "/hero"
    });

    const contentfulEnhancer = createContentfulEnhancer({ client });
    
    await enhance({
      composition,
      enhancers: new EnhancerBuilder().parameterType(
        CANVAS_CONTENTFUL_PARAMETER_TYPES,
        contentfulEnhancer
      ),
      context: {}
    });

    return { composition };
  }
};
</script>
