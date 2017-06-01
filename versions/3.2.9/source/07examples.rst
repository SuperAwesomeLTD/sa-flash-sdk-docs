Examples
========

Simple example
^^^^^^^^^^^^^^

The first example shows how you can add a video ad in your app with just a
few lines of code.

.. code-block:: actionscript

    package {

        import flash.display.MovieClip;
        import flash.geom.Rectangle;

        // superawesome imports
        import tv.superawesome.sdk.*;
        import tv.superawesome.sdk.Loader.SALoader;
        import tv.superawesome.sdk.Loader.SALoaderInterface;
        import tv.superawesome.sdk.Models.SAAd;
        import tv.superawesome.sdk.Views.SAAdInterface;
        import tv.superawesome.sdk.Views.SAVideoAd;

        public class AdobeFlashDemo
               extends Sprite
               implements SALoaderInterface {

            // declare the three main variables
            // needed by SuperAwesome to load & display
            // an Ad
            private var loader: SALoader = null;
            private var video: SAVideoAd = null;
            private var adData: SAAd = null;

            public function AdobeFlashDemo() {

                // config SuperAwesome
                SuperAwesome.getInstance().setConfigurationProduction();
                SuperAwesome.getInstance().enableTestMode();

                // load the ad
                loader = new SALoader();
                loader.delegate = this;
                loader.loadAd(30479);
            }

            // implementation of the SALoaderInterface
            public function didLoadAd(ad: SAAd): void {
                // handle success
                adData = ad;

                var frame = new Rectangle(0, 50, 640, 400);
                video = new SAVideoAd(frame);
                video.setAd(adData);
                addChildAd(video, 0);
                video.play();
            }

            public function didFailToLoadAd(placementId: int): void {
                // failure
            }
        }
    }

Complex example
^^^^^^^^^^^^^^^

This example shows how you can add different types of ads and make them respond to
multiple callbacks.

.. code-block:: actionscript

    package {

        import flash.display.MovieClip;
        import flash.geom.Rectangle;

        // superawesome imports
        import tv.superawesome.sdk.*;
        import tv.superawesome.sdk.Models.SAAd;
        import tv.superawesome.sdk.Loader.SALoader;
        import tv.superawesome.sdk.Views.SABannerAd;
        import tv.superawesome.sdk.Views.SAVideoAd;
        import tv.superawesome.sdk.Loader.SALoaderInterface;
        import tv.superawesome.sdk.Views.SAAdInterface;
        import tv.superawesome.sdk.Views.SAVideoAdInterface;

        public class AdobeFlashDemo
               extends Sprite
               implements SALoaderInterface,
                          SAAdInterface,
                          SAVideoAdInterface {

            // loader
            private var loader: SALoader = null;

            // ad data
            private var bannerAdData: SAAd = null;
            private var videoAdData: SAAd = null;

            // display objects
            private var banner: SABannerAd = null;
            private var video: SAVideoAd = null;

            public function AdobeFlashDemo() {
                // config SuperAwesome
                SuperAwesome.getInstance().setConfigurationProduction();
                SuperAwesome.getInstance().enableTestMode();

                // load the ad
                loader = new SALoader();
                loader.delegate = this;
                loader.loadAd(30471);
                loader.loadAd(30479);
            }

            //
            // three function to display ads -
            // these should be connected to buttons
            public function showBanner(): void {
                var frame = new Rectangle(0, 0, 320, 50);

                // it's good practice to always check
                // that the ad data is not null
                if (bannerAdData) {
                    banner = new SABannerAd(frame);
                    banner.setAd(bannerAdData);
                    banner.adDelegate = this;
                    addChildAt(banner, 0);
                    banner.play();
                }
            }

            public function showVideo(): void {
                if (videoAdData) {
                    video = new SAFullscreenVideoAd();
                    video.setAd(ad);
                    video.adDelegate = this;
                    video.videoDelegate = this;
                    video.play();
                }
            }

            //
            // SAAdInterface implementation
            public function adWasShown(placementId: int): void {
                trace("Ad " + placementId + " Was shown");
            }

            public function adFailedToShow(placementId: int): void {}
            public function adWasClosed(placementId: int): void {}
            public function adWasClicked(placementId: int): void {}
            public function adHasIncorrectPlacement(placementId: int): void {}

            //
            // SAVideoAdInterface implementation
            public function adStarted(placementId: int): void {}
            public function videoStarted(placementId: int): void {}
            public function videoReachedFirstQuartile(placementId: int): void {}

            public function videoReachedMidpoint(placementId: int): void {
                trace("Reached midpoint with " + placementId);
            }

            public function videoReachedThirdQuartile(placementId: int): void {}
            public function videoEnded(placementId: int): void {}
            public function adEnded(placementId: int): void {}

            public function allAdsEnded(placementId: int): void {
                trace("All video ads ended!");
            }
        }
    }
