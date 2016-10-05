Display ads
===========

In the next sections we'll see how to display banners and video ads.

We'll assume we have the same setup as the previous section, but we'll also add
two SuperAwesome display objects that we'll want to show at the press of a button
in our app.

.. code-block:: actionscript

    import tv.superawesome.*

    public class AdobeFlashDemo
           extends Sprite
           implements SALoaderInterface {

        // the loader object
        private var loader: SALoader = null;

        // ad data
        private var bannerAdData: SAAd = null;
        private var videoAdData: SAAd = null;

        // the four display objects
        private var banner: SABannerAd = null;
        private var video: SAVideoAd = null;
    }

Banner ads
^^^^^^^^^^

To following code snippet shows you how to add a **SABannerAd** object to your app.

.. code-block:: actionscript

    public class AdobeFlashDemo
           extends Sprite
           implements SALoaderInterface {

        // load ad data here ...

        public function showBanner() {
            if (bannerAdData != null) {
                var frame = new Rectangle(250, 450, 640, 100);
                banner = new SABannerAd(frame);
                banner.setAd(bannerAdData);
                addChildAt(banner, 0);
                banner.play();
            }
        }
    }

Notice that the SABannerAd class is itself descended from **Sprite** so it must be added to the scene.

The two functions to pay attention here are **setAd(SAAd ad)** and **play()**.

* **setAd(SAAd ad)** takes a SAAd object as parameter, in this case bannerAdData. It tells the banner what ad data to try to display.
* **play()** actually starts the display process on screen.

Video ads
^^^^^^^^^

**SAVideoAd** gets initialized and added in a similar way:

.. code-block:: actionscript

    public class AdobeFlashDemo
           extends Sprite
           implements SALoaderInterface {

        // load ad data here ...

        public function showInLineVideo() {
            if (videoAdData != null) {
                var frame = new Rectangle(250, 450, 640, 100);
                video = new SAVideoAd(frame);
                video.setAd(videoAdData);

                // toggles a small video "click" button
                // instead of the whole video surface
                video.shouldShowSmallClickButton = true;

                addChildAt(video, 0);
                vidoe.play();
            }
        }
    }

As with SABannerAd, the SAVideoAd object must be added to the view hierarchy.
It also implements the same two functions: setAd(SAAd ad) and play().
