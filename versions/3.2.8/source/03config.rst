Configure the SDK
=================

Once you've integrated the SuperAwesome SDK, you can access all functionality by including the SuperAwesome swc library in any actionscript file you want
to use it.

.. code-block:: actionscript

    import tv.superawesome.*

or including one of the relevant headers

.. code-block:: actionscript

    import tv.superawesome.sdk.*;
    import tv.superawesome.sdk.Loader.*;
    import tv.superawesome.sdk.Models.*;
    import tv.superawesome.sdk.Loader.SALoaderInterface;
    import tv.superawesome.sdk.Models.SAAd;
    import tv.superawesome.sdk.Views.SAVideoAdInterface;
    import tv.superawesome.sdk.Views.SAAdInterface;
    import tv.superawesome.sdk.Views.SABannerAd;
    import tv.superawesome.sdk.Views.SAVideoAd;

There are also a few global SDK parameters you can change according to your needs:

=============  ==============  =======
Parameter      Values          Meaning
=============  ==============  =======
Configuration  | Production *  | Should always get ads from production server

Test mode      | Enabled       | Should the SDK serve test ads. For test
               | Disabled *    | placements (30471, 30476, etc) must be Enabled.
=============  ==============  =======
 * = denotes default values

You can leave these settings as they are or change them to fit your testing or production needs, as follows:

.. code-block:: actionscript

    // Import all the SuperAwesome SDK library
    // with all subsequent namespaces
    import tv.superawesome.*

    //
    // AdobeFlashDemo is a generic
    // Flash Professional CC project
    public class AdobeFlashDemo
            extends Sprite {

        public function AdobeAIRDemo() {

            SuperAwesome.getInstance().setConfigurationProduction();
            SuperAwesome.getInstance().enableTestMode();
            // SuperAwesome.getInstance().disableTestMode();
        }
    }
