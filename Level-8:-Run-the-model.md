	cd $EXP
	mpirun -n 4 ./opa

**Additional Notes:**

With Anthony's help I got NEMO to run properly. There were issues with the namelist_cfg, file_def_nemo.xml and field_def_nemo-opa.xml files. I copied Anthony's xml files as I wasn't able to figure out the issues with the file xml file, I am pretty sure there was a file tag misplaced somewhere but life is too short anyway here is the file_def_nemo.xml file::

	<?xml version="1.0"?>

	    <!-- 
	============================================================================================================
	=                                           output files definition                                        =
	=                                            Define your own files                                         =
	=                                         put the variables you want...                                    =
	============================================================================================================
	    -->
	    
	    <file_definition type="one_file" name="@expname@_@freq@_@startdate@_@enddate@" sync_freq="10d" min_digits="4">
	    
	      <file_group id="1ts" output_freq="1ts"  output_level="10" enabled=".TRUE."/> <!-- 1 time step files -->

	      <file_group id="1h" output_freq="1h"  output_level="10" enabled=".TRUE."> <!-- 1h files -->
	 	<file id="file19" name_suffix="_SSH" description="ocean T grid variables" >
	          <field field_ref="ssh"          name="zos" operation="instant"  />
	  	</file>


	<!-- Old tidal harmonic output style
	        <file id="file20" name_suffix="_Tides" description="tidal harmonics" >
	          <field field_ref="M2x"          name="M2x"      long_name="M2 Elevation harmonic real part"                       />
	          <field field_ref="M2y"          name="M2y"      long_name="M2 Elevation harmonic imaginary part"                  />
		  <field field_ref="S2x"          name="S2x"      long_name="S2 Elevation harmonic real part"                       />
	          <field field_ref="S2y"          name="S2y"      long_name="S2 Elevation harmonic imaginary part"                  />
		  <field field_ref="K2x"          name="K2x"      long_name="K2 Elevation harmonic real part"                       />
	          <field field_ref="K2y"          name="K2y"      long_name="K2 Elevation harmonic imaginary part"                  />
	-->          
	<!--	  <field field_ref="M2x_u"        name="M2x_u"    long_name="M2 current barotrope along i-axis harmonic real part "       />
	          <field field_ref="M2y_u"        name="M2y_u"    long_name="M2 current barotrope along i-axis harmonic imaginary part "  />

	          <field field_ref="M2x_v"        name="M2x_v"    long_name="M2 current barotrope along j-axis harmonic real part "       />
	          <field field_ref="M2y_v"        name="M2y_v"    long_name="M2 current barotrope along j-axis harmonic imaginary part "  />
	-->
	<!--        </file>  -->
	      </file_group>

	      <file_group id="2h" output_freq="2h"  output_level="10" enabled=".TRUE."/> <!-- 2h files -->
	      <file_group id="3h" output_freq="3h"  output_level="10" enabled=".TRUE."/> <!-- 3h files -->     
	      <file_group id="4h" output_freq="4h"  output_level="10" enabled=".TRUE."/> <!-- 4h files -->
	      <file_group id="6h" output_freq="6h"  output_level="10" enabled=".TRUE."/> <!-- 6h files -->     
	      <file_group id="1d" output_freq="1d"  output_level="10" enabled=".TRUE."> <!-- 1d files -->
	<!--	<file id="file19" name_suffix="_SSH" description="ocean T grid variables" >
	         <field field_ref="ssh"          name="zos"   /> 
	        </file> -->
	      </file_group>
	      <file_group id="3d" output_freq="3d"  output_level="10" enabled=".TRUE."/> <!-- 3d files -->
	      <file_group id="5d" output_freq="5d"  output_level="10" enabled=".TRUE.">  <!-- 5d files -->   

	<!--
		<file id="file20" name_suffix="_Tides" description="tidal harmonics" >
		  <field field_ref="M2x"          name="M2x"      long_name="M2 Elevation harmonic real part"                       />
		  <field field_ref="M2y"          name="M2y"      long_name="M2 Elevation harmonic imaginary part"                  />
		  <field field_ref="M2x_u"        name="M2x_u"    long_name="M2 current barotrope along i-axis harmonic real part "       />
		  <field field_ref="M2y_u"        name="M2y_u"    long_name="M2 current barotrope along i-axis harmonic imaginary part "  />

		  <field field_ref="M2x_v"        name="M2x_v"    long_name="M2 current barotrope along j-axis harmonic real part "       />
		  <field field_ref="M2y_v"        name="M2y_v"    long_name="M2 current barotrope along j-axis harmonic imaginary part "  />
		</file>
	-->
	<!--
	        <file id="file11" name_suffix="_Tides_T" >
	          <field field_ref="M2x"     name="M2_x_elev"  />
	          <field field_ref="M2y"     name="M2_y_elev"  />
	          <field field_ref="S2x"     name="S2_x_elev"  />
	          <field field_ref="S2y"     name="S2_y_elev"  />
	          <field field_ref="N2x"     name="N2_x_elev"  />
	          <field field_ref="N2y"     name="N2_y_elev"  />
	          <field field_ref="K2x"     name="K2_x_elev"  />
	          <field field_ref="K2y"     name="K2_y_elev"  />
	          <field field_ref="K1x"     name="K1_x_elev"  />
	          <field field_ref="K1y"     name="K1_y_elev"  />
	          <field field_ref="M4x"     name="M4_x_elev"  />
	          <field field_ref="M4y"     name="M4_y_elev"  />
	          <field field_ref="Q1x"     name="Q1_x_elev"  />
	          <field field_ref="Q1y"     name="Q1_y_elev"  />
	          <field field_ref="O1x"     name="O1_x_elev"  />
	          <field field_ref="O1y"     name="O1_y_elev"  />
	          <field field_ref="P1x"     name="P1_x_elev"  />
	          <field field_ref="P1y"     name="P1_y_elev"  />
	          <field field_ref="S1x"     name="S1_x_elev"  />
	          <field field_ref="S1y"     name="S1_y_elev"  />
	          <field field_ref="2N2x"    name="a2N2_x_elev"  />
	          <field field_ref="2N2y"    name="a2N2_y_elev"  />
	          <field field_ref="MU2x"    name="MU2_x_elev"  />
	          <field field_ref="MU2y"    name="MU2_y_elev"  />
	          <field field_ref="NU2x"    name="NU2_x_elev"  />
	          <field field_ref="NU2y"    name="NU2_y_elev"  />
	          <field field_ref="L2x"     name="L2_x_elev"  />
	          <field field_ref="L2y"     name="L2_y_elev"  />
	          <field field_ref="T2x"     name="T2_x_elev"  />
	          <field field_ref="T2y"     name="T2_y_elev"  />
	        </file>

	        <file id="file12" name_suffix="_Tides_U" >
	          <field field_ref="M2x_u"     name="M2_x_u"  />
	          <field field_ref="M2y_u"     name="M2_y_u"  />
	          <field field_ref="S2x_u"     name="S2_x_u"  />
	          <field field_ref="S2y_u"     name="S2_y_u"  />
	          <field field_ref="N2x_u"     name="N2_x_u"  />
	          <field field_ref="N2y_u"     name="N2_y_u"  />
	          <field field_ref="K2x_u"     name="K2_x_u"  />
	          <field field_ref="K2y_u"     name="K2_y_u"  />
	          <field field_ref="K1x_u"     name="K1_x_u"  />
	          <field field_ref="K1y_u"     name="K1_y_u"  />
	          <field field_ref="M4x_u"     name="M4_x_u"  />
	          <field field_ref="M4y_u"     name="M4_y_u"  />
	          <field field_ref="Q1x_u"     name="Q1_x_u"  />
	          <field field_ref="Q1y_u"     name="Q1_y_u"  />
	          <field field_ref="O1x_u"     name="O1_x_u"  />
	          <field field_ref="O1y_u"     name="O1_y_u"  />
	          <field field_ref="P1x_u"     name="P1_x_u"  />
	          <field field_ref="P1y_u"     name="P1_y_u"  />
	          <field field_ref="S1x_u"     name="S1_x_u" />
	          <field field_ref="S1y_u"     name="S1_y_u" />
	          <field field_ref="2N2x_u"    name="a2N2_x_u" />
	          <field field_ref="2N2y_u"    name="a2N2_y_u" />
	          <field field_ref="MU2x_u"    name="MU2_x_u" />
	          <field field_ref="MU2y_u"    name="MU2_y_u" />
	          <field field_ref="NU2x_u"    name="NU2_x_u" />
	          <field field_ref="NU2y_u"    name="NU2_y_u" />
	          <field field_ref="L2x_u"     name="L2_x_u" />
	          <field field_ref="L2y_u"     name="L2_y_u" />
	          <field field_ref="T2x_u"     name="T2_x_u" />
	          <field field_ref="T2y_u"     name="T2_y_u" />
	        </file>

	        <file id="file13" name_suffix="_Tides_V" >
	          <field field_ref="M2x_v"     name="M2_x_v"  />
	          <field field_ref="M2y_v"     name="M2_y_v"  />
	          <field field_ref="S2x_v"     name="S2_x_v"  />
	          <field field_ref="S2y_v"     name="S2_y_v"  />
	          <field field_ref="N2x_v"     name="N2_x_v"  />
	          <field field_ref="N2y_v"     name="N2_y_v"  />
	          <field field_ref="K2x_v"     name="K2_x_v"  />
	          <field field_ref="K2y_v"     name="K2_y_v"  />
	          <field field_ref="K1x_v"     name="K1_x_v"  />
	          <field field_ref="K1y_v"     name="K1_y_v"  />
	          <field field_ref="M4x_v"     name="M4_x_v"  />
	          <field field_ref="M4y_v"     name="M4_y_v"  />
	          <field field_ref="Q1x_v"     name="Q1_x_v"  />
	          <field field_ref="Q1y_v"     name="Q1_y_v"  />
	          <field field_ref="O1x_v"     name="O1_x_v"  />
	          <field field_ref="O1y_v"     name="O1_y_v"  />
	          <field field_ref="P1x_v"     name="P1_x_v"  />
	          <field field_ref="P1y_v"     name="P1_y_v"  />
	          <field field_ref="S1x_v"     name="S1_x_v" />
	          <field field_ref="S1y_v"     name="S1_y_v" />
	          <field field_ref="2N2x_v"    name="a2N2_x_v" />
	          <field field_ref="2N2y_v"    name="a2N2_y_v" />
	          <field field_ref="MU2x_v"    name="MU2_x_v" />
	          <field field_ref="MU2y_v"    name="MU2_y_v" />
	          <field field_ref="NU2x_v"    name="NU2_x_v" />
	          <field field_ref="NU2y_v"    name="NU2_y_v" />
	          <field field_ref="L2x_v"     name="L2_x_v" />
	          <field field_ref="L2y_v"     name="L2_y_v" />
	          <field field_ref="T2x_v"     name="T2_x_v" />
	          <field field_ref="T2y_v"     name="T2_y_v" />
	        </file>
	-->
	      </file_group>

	      <file_group id="tidal_harmonics" output_freq="1h"  output_level="10" enabled=".TRUE."> <!-- 1d files -->

	        <file id="tidalanalysis.grid_T" name="harmonic_grid_T" description="ocean T grid variables"  enabled=".TRUE.">

	          <field field_ref="O1amp"         name="O1amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="O1phase"       name="O1phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="K1amp"         name="K1amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="K1phase"       name="K1phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="Q1amp"         name="Q1amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="Q1phase"       name="Q1phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="P1amp"         name="P1amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="P1phase"       name="P1phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="M2amp"         name="M2amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="M2phase"       name="M2phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="S2amp"         name="S2amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="S2phase"       name="S2phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="N2amp"         name="N2amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="N2phase"       name="N2phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="K2amp"         name="K2amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="K2phase"       name="K2phase"     operation="instant" enabled=".TRUE." />
	          <field field_ref="M4amp"         name="M4amp"       operation="instant" enabled=".TRUE." />
	          <field field_ref="M4phase"       name="M4phase"     operation="instant" enabled=".TRUE." />

	        </file>
	      </file_group>

	      <file_group id="1m" output_freq="1mo" output_level="10" enabled=".TRUE."/> <!-- real monthly files -->
	      <file_group id="2m" output_freq="2mo" output_level="10" enabled=".TRUE."/> <!-- real 2m files -->
	      <file_group id="3m" output_freq="3mo" output_level="10" enabled=".TRUE."/> <!-- real 3m files -->
	      <file_group id="4m" output_freq="4mo" output_level="10" enabled=".TRUE."/> <!-- real 4m files -->
	      <file_group id="6m" output_freq="6mo" output_level="10" enabled=".TRUE."/> <!-- real 6m files -->
	      <file_group id="1y"  output_freq="1y" output_level="10" enabled=".TRUE."/> <!-- real yearly files -->
	      <file_group id="2y"  output_freq="2y" output_level="10" enabled=".TRUE."/> <!-- real 2y files -->
	      <file_group id="5y"  output_freq="5y" output_level="10" enabled=".TRUE."/> <!-- real 5y files -->
	      <file_group id="10y" output_freq="10y" output_level="10" enabled=".TRUE."/> <!-- real 10y files -->

	   </file_definition>
    
The field xml file also needed editing as the tide harmonic fields such as O1amp where not present for some reason? Anyway here is the file::

	<?xml version="1.0"?> 
	    <!-- $id$ -->
	    
	    <!-- 
	============================================================================================================
	=                                  definition of all existing variables                                    =
	=                                            DO NOT CHANGE                                                 =
	============================================================================================================
	    -->
	   <field_definition level="1" prec="4" operation="average" enabled=".TRUE." default_value="1.e20" > <!-- time step automaticaly defined -->

	    <!-- 
	============================================================================================================
	                                  Physical ocean model variables
	============================================================================================================
	    -->

	      <!-- T grid -->
	      
	      <field_group id="grid_T" grid_ref="grid_T_2D" >
	         <field id="e3t"          long_name="T-cell thickness"   standard_name="cell_thickness"   unit="m"   grid_ref="grid_T_3D"/>
	         <field id="e3t_surf"     long_name="T-cell thickness"   field_ref="e3t"  standard_name="cell_thickness"   unit="m"   grid_ref="grid_T_SFC"/>
	         <field id="e3t_0"        long_name="Initial T-cell thickness"   standard_name="ref_cell_thickness"   unit="m"   grid_ref="grid_T_3D"/>

	         <field id="toce"         long_name="temperature"         standard_name="sea_water_potential_temperature"   unit="degC"     grid_ref="grid_T_3D"/>
	         <field id="toce_e3t"     long_name="temperature (thickness weighted)"                                      unit="degC"     grid_ref="grid_T_3D" > toce * e3t </field >
	         <field id="soce"         long_name="salinity"            standard_name="sea_water_practical_salinity"      unit="1e-3"     grid_ref="grid_T_3D"/>
	         <field id="soce_e3t"     long_name="salinity    (thickness weighted)"                                      unit="1e-3"     grid_ref="grid_T_3D" > soce * e3t </field >

	         <!-- t-eddy viscosity coefficients (ldfdyn) -->
		 <field id="ahmt_2d"      long_name=" surface t-eddy viscosity coefficient"   unit="m2/s or m4/s" />
		 <field id="ahmt_3d"      long_name=" 3D      t-eddy viscosity coefficient"   unit="m2/s or m4/s"                           grid_ref="grid_T_3D"/>

	         <field id="sst"          long_name="sea surface temperature"             standard_name="sea_surface_temperature"             unit="degC"     />
	         <field id="sst2"         long_name="square of sea surface temperature"   standard_name="square_of_sea_surface_temperature"   unit="degC2"     > sst * sst </field >
	         <field id="sstmax"       long_name="max of sea surface temperature"   field_ref="sst"   operation="maximum"                                  />
	         <field id="sstmin"       long_name="min of sea surface temperature"   field_ref="sst"   operation="minimum"                                  />
	         <field id="sstgrad"      long_name="module of sst gradient"                                                                  unit="degC/m"   />
	         <field id="sstgrad2"     long_name="square of module of sst gradient"                                                        unit="degC2/m2" />
	         <field id="sbt"          long_name="sea bottom temperature"                                                                  unit="degC"     />
	         <field id="tosmint"      long_name="vertical integral of temperature times density"   standard_name="integral_wrt_depth_of_product_of_density_and_potential_temperature"  unit="(kg m2) degree_C" />
	         <field id="sst_wl"       long_name="Delta SST of warm layer"                                                                 unit="degC"     />
	         <field id="sst_cs"       long_name="Delta SST of cool skin"                                                                  unit="degC"     />
		 <field id="temp_3m"      long_name="temperature at 3m"                                                                       unit="degC"     />
	         
	         <field id="sss"          long_name="sea surface salinity"             standard_name="sea_surface_salinity"   unit="1e-3" />
	         <field id="sss2"         long_name="square of sea surface salinity"                                          unit="1e-6"  > sss * sss </field >
	         <field id="sssmax"       long_name="max of sea surface salinity"   field_ref="sss"   operation="maximum"                 />
	         <field id="sssmin"       long_name="min of sea surface salinity"   field_ref="sss"   operation="minimum"                 />
	         <field id="sbs"          long_name="sea bottom salinity"                                                     unit="0.001" />
	         <field id="somint"       long_name="vertical integral of salinity times density"   standard_name="integral_wrt_depth_of_product_of_density_and_salinity"  unit="(kg m2) x (1e-3)" /> 

	         <field id="taubot"       long_name="bottom stress module"                                                    unit="N/m2" /> 

	         <field id="ssh"          long_name="sea surface height"             standard_name="sea_surface_height_above_geoid"             unit="m" />
	         <field id="ssh2"         long_name="square of sea surface height"   standard_name="square_of_sea_surface_height_above_geoid"   unit="m2" > ssh * ssh </field >
	         <field id="wetdep"       long_name="wet depth"                      standard_name="wet_depth"                unit="m" />
	         <field id="sshmax"       long_name="max of sea surface height"   field_ref="ssh"   operation="maximum"                                  />

	         <field id="mldkz5"       long_name="Turbocline depth (Kz = 5e-4)"                       standard_name="ocean_mixed_layer_thickness_defined_by_vertical_tracer_diffusivity"                unit="m"          />
	         <field id="mldr10_1"     long_name="Mixed Layer Depth (dsigma = 0.01 wrt 10m)"          standard_name="ocean_mixed_layer_thickness_defined_by_sigma_theta"                                unit="m"          />
	         <field id="mldr10_1max"  long_name="Max of Mixed Layer Depth (dsigma = 0.01 wrt 10m)"   field_ref="mldr10_1"   operation="maximum"                                                                          />
	         <field id="mldr10_1min"  long_name="Min of Mixed Layer Depth (dsigma = 0.01 wrt 10m)"   field_ref="mldr10_1"   operation="minimum"                                                                          />
	         <field id="heatc"        long_name="Heat content vertically integrated"                 standard_name="integral_of_sea_water_potential_temperature_wrt_depth_expressed_as_heat_content"   unit="J/m2"       />
	         <field id="saltc"        long_name="Salt content vertically integrated"                                                                                                                   unit="1e-3*kg/m2" />

	         <!-- EOS -->
	         <field id="alpha"        long_name="thermal expansion"                                                         unit="degC-1" grid_ref="grid_T_3D" />
	         <field id="beta"         long_name="haline contraction"                                                        unit="1e3"    grid_ref="grid_T_3D" />
	         <field id="bn2"          long_name="squared Brunt-Vaisala frequency"                                           unit="s-1"    grid_ref="grid_T_3D" />
	         <field id="rhop"         long_name="potential density (sigma0)"        standard_name="sea_water_sigma_theta"   unit="kg/m3"  grid_ref="grid_T_3D" />

	         <!-- Energy - horizontal divergence -->
	         <field id="eken"         long_name="kinetic energy"          standard_name="specific_kinetic_energy_of_sea_water"   unit="m2/s2"  grid_ref="grid_T_3D" />
	         <field id="hdiv"         long_name="horizontal divergence"                                                          unit="s-1"    grid_ref="grid_T_3D" />

	         <!-- variables available with MLE -->
	         <field id="Lf_NHpf"      long_name="MLE: Lf = N H / f"   unit="m" />

	         <!-- next variables available with key_diahth -->
	         <field id="mlddzt"       long_name="Thermocline Depth (depth of max dT/dz)"         standard_name="depth_at_maximum_upward_derivative_of_sea_water_potential_temperature"             unit="m"                         />
	         <field id="mldr10_3"     long_name="Mixed Layer Depth (dsigma = 0.03 wrt 10m)"      standard_name="ocean_mixed_layer_thickness_defined_by_sigma_theta"                                unit="m"                         />
	         <field id="mldr0_1"      long_name="Mixed Layer Depth (dsigma = 0.01 wrt sfc)"      standard_name="ocean_mixed_layer_thickness_defined_by_sigma_theta"                                unit="m"                         />
	         <field id="mldr0_3"      long_name="Mixed Layer Depth (dsigma = 0.03 wrt sfc)"      standard_name="ocean_mixed_layer_thickness_defined_by_sigma_theta"                                unit="m"                         />
	         <field id="mld_dt02"     long_name="Mixed Layer Depth (|dT| = 0.2 wrt 10m)"         standard_name="ocean_mixed_layer_thickness_defined_by_temperature"                                unit="m"                         />
	         <field id="topthdep"     long_name="Top of Thermocline Depth (dT = -0.2 wrt 10m)"   standard_name="ocean_mixed_layer_thickness_defined_by_temperature"                                unit="m"                         />
	         <field id="pycndep"      long_name="Pycnocline Depth (dsigma[dT=-0.2] wrt 10m)"     standard_name="ocean_mixed_layer_thickness_defined_by_sigma_theta"                                unit="m"                         />
	         <field id="BLT"          long_name="Barrier Layer Thickness"                                                                                                                          unit="m"                          > topthdep - pycndep </field>
	         <field id="tinv"         long_name="Max of vertical invertion of temperature"                                                                                                         unit="degC"                      />
	         <field id="depti"        long_name="Depth of max. vert. inv. of temperature"                                                                                                          unit="m"                         />
	         <field id="20d"          long_name="Depth of 20C isotherm"                          standard_name="depth_of_isosurface_of_sea_water_potential_temperature"                            unit="m"      axis_ref="iax_20C" />
	         <field id="28d"          long_name="Depth of 28C isotherm"                          standard_name="depth_of_isosurface_of_sea_water_potential_temperature"                            unit="m"      axis_ref="iax_28C" />
	         <field id="hc300"        long_name="Heat content 0-300m"                            standard_name="integral_of_sea_water_potential_temperature_wrt_depth_expressed_as_heat_content"   unit="J/m2"                      />

	         <!-- variables available with diaar5 -->
	         <field id="botpres"      long_name="Sea Water Pressure at Sea Floor"   standard_name="sea_water_pressure_at_sea_floor"   unit="dbar" />
	         <field id="sshdyn"       long_name="dynamic sea surface height"     standard_name="dynamic_sea_surface_height_above_geoid"     unit="m" />
	         <field id="sshdyn2"      long_name="square of dynamic sea surface height"     standard_name="dynamic_sea_surface_height_above_geoid_squared"     unit="m2" > sshdyn * sshdyn </field>
	         <field id="tnpeo"      long_name="Tendency of ocean potential energy content"          unit="W/m2"                           />

	         <!-- variables available ln_linssh=.FALSE. -->
	         <field id="tpt_dep"      long_name="T-point depth"                  standard_name="depth_below_geoid"   unit="m"   grid_ref="grid_T_3D" />
	         <field id="e3tdef"       long_name="T-cell thickness deformation"                                       unit="%"   grid_ref="grid_T_3D" />
	      </field_group>

	      <!-- Tides -->

	      <field_group id="Tides_T" grid_ref="grid_T_2D" operation="once" >
	         <!-- tidal composante -->
	         <field id="M2x"          long_name="M2 Elevation harmonic real part "                             unit="m"        />
	         <field id="M2y"          long_name="M2 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="S2x"          long_name="S2 Elevation harmonic real part "                             unit="m"        />
	         <field id="S2y"          long_name="S2 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="N2x"          long_name="N2 Elevation harmonic real part "                             unit="m"        />
	         <field id="N2y"          long_name="N2 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="K1x"          long_name="K1 Elevation harmonic real part "                             unit="m"        />
	         <field id="K1y"          long_name="K1 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="O1x"          long_name="O1 Elevation harmonic real part "                             unit="m"        />
	         <field id="O1y"          long_name="O1 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="Q1x"          long_name="Q1 Elevation harmonic real part "                             unit="m"        />
	         <field id="Q1y"          long_name="Q1 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="M4x"          long_name="M4 Elevation harmonic real part "                             unit="m"        />
	         <field id="M4y"          long_name="M4 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="K2x"          long_name="K2 Elevation harmonic real part "                             unit="m"        />
	         <field id="K2y"          long_name="K2 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="P1x"          long_name="P1 Elevation harmonic real part "                             unit="m"        />
	         <field id="P1y"          long_name="P1 Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="Mfx"          long_name="Mf Elevation harmonic real part "                             unit="m"        />
	         <field id="Mfy"          long_name="Mf Elevation harmonic imaginary part"                         unit="m"        />
	         <field id="Mmx"          long_name="Mm Elevation harmonic real part "                             unit="m"        />
	         <field id="Mmy"          long_name="Mm Elevation harmonic imaginary part"                         unit="m"        />
	        
		 <field id="M2amp"        long_name="M2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="M2phase"      long_name="M2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="S2amp"        long_name="S2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="S2phase"      long_name="S2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="N2amp"        long_name="N2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="N2phase"      long_name="N2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="K1amp"        long_name="K1 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="K1phase"      long_name="K1 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="O1amp"        long_name="O1 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="O1phase"      long_name="O1 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="Q1amp"        long_name="Q1 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="Q1phase"      long_name="Q1 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="M4amp"        long_name="M4 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="M4phase"      long_name="M4 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="MS4amp"        long_name="MS4 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="MS4phase"      long_name="MS4 Elevation harmonic Phase"                                  unit="degree"   />
	                                                                           
	         <field id="MN4amp"        long_name="MN4 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="MN4phase"      long_name="MN4 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="K2amp"        long_name="K2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="K2phase"      long_name="K2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="P1amp"        long_name="P1 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="P1phase"      long_name="P1 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="Mfamp"        long_name="Mf Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="Mfphase"      long_name="Mf Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="Mmamp"        long_name="Mm Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="Mmphase"      long_name="Mm Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="T2amp"        long_name="T2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="T2phase"      long_name="T2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="L2amp"        long_name="L2 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="L2phase"      long_name="L2 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="S1amp"        long_name="S1 Elevation harmonic Amplitude"                              unit="m"        />
	         <field id="S1phase"      long_name="S1 Elevation harmonic Phase"                                  unit="degree"   />

	         <field id="2N2amp"       long_name="2N2 Elevation harmonic Amplitude"                             unit="m"        />
	         <field id="2N2phase"     long_name="2N2 Elevation harmonic Phase"                                 unit="degree"   />

	         <field id="MU2amp"       long_name="MU2 Elevation harmonic Amplitude"                             unit="m"        />
	         <field id="MU2phase"     long_name="MU2 Elevation harmonic Phase"                                 unit="degree"   />

	         <field id="NU2amp"       long_name="NU2 Elevation harmonic Amplitude"                             unit="m"        />
	         <field id="NU2phase"     long_name="NU2 Elevation harmonic Phase"                                 unit="degree"   />
	                                                                                                   
	      </field_group>
		 
	      <field_group id="Tides_U" grid_ref="grid_U_2D" operation="once" >
	         <field id="M2x_u"        long_name="M2 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="M2y_u"        long_name="M2 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="S2x_u"        long_name="S2 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="S2y_u"        long_name="S2 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="N2x_u"        long_name="N2 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="N2y_u"        long_name="N2 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="K1x_u"        long_name="K1 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="K1y_u"        long_name="K1 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="O1x_u"        long_name="O1 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="O1y_u"        long_name="O1 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Q1x_u"        long_name="Q1 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="Q1y_u"        long_name="Q1 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="M4x_u"        long_name="M4 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="M4y_u"        long_name="M4 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="K2x_u"        long_name="K2 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="K2y_u"        long_name="K2 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="P1x_u"        long_name="P1 current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="P1y_u"        long_name="P1 current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Mfx_u"        long_name="Mf current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="Mfy_u"        long_name="Mf current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Mmx_u"        long_name="Mm current barotrope along i-axis harmonic real part "        unit="m/s"      />
	         <field id="Mmy_u"        long_name="Mm current barotrope along i-axis harmonic imaginary part "   unit="m/s"      />
	      
	         <field id="M2amp_u2D"      long_name="M2 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="M2phase_u2D"    long_name="M2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="S2amp_u2D"      long_name="S2 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="S2phase_u2D"    long_name="S2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="N2amp_u2D"      long_name="N2 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="N2phase_u2D"    long_name="N2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="K1amp_u2D"      long_name="K1 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="K1phase_u2D"    long_name="K1 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="O1amp_u2D"      long_name="O1 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="O1phase_u2D"    long_name="O1 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Q1amp_u2D"      long_name="Q1 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Q1phase_u2D"    long_name="Q1 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="M4amp_u2D"      long_name="M4 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="M4phase_u2D"    long_name="M4 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="MS4amp_u2D"      long_name="MS4 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="MS4phase_u2D"    long_name="MS4 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="MN4amp_u2D"      long_name="MN4 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="MN4phase_u2D"    long_name="MN4 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="K2amp_u2D"      long_name="K2 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="K2phase_u2D"    long_name="K2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="P1amp_u2D"      long_name="P1 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="P1phase_u2D"    long_name="P1 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Mfamp_u2D"      long_name="Mf U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Mfphase_u2D"    long_name="Mf U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Mmamp_u2D"      long_name="Mm U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Mmphase_u2D"    long_name="Mm U barotropic harmonic Phase"                               unit="degree"   />
	         <field id="T2amp_u2D"      long_name="T2 U barotropic harmonic Amplitude"                           unit="m/s"      />

	         <field id="T2phase_u2D"    long_name="T2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="L2amp_u2D"      long_name="L2 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="L2phase_u2D"    long_name="L2 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="S1amp_u2D"      long_name="S1 U barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="S1phase_u2D"    long_name="S1 U barotropic harmonic Phase"                               unit="degree"   />

	         <field id="2N2amp_u2D"     long_name="2N2 U barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="2N2phase_u2D"   long_name="2N2 U barotropic harmonic Phase"                              unit="degree"   />

	         <field id="MU2amp_u2D"     long_name="MU2 U barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="MU2phase_u2D"   long_name="MU2 U barotropic harmonic Phase"                              unit="degree"   />

	         <field id="NU2amp_u2D"     long_name="NU2 U barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="NU2phase_u2D"   long_name="NU2 U barotropic harmonic Phase"                              unit="degree"   />

	      </field_group>
		 
	      <field_group id="Tides_V" grid_ref="grid_V_2D" operation="once" >
	         <field id="M2x_v"        long_name="M2 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="M2y_v"        long_name="M2 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="S2x_v"        long_name="S2 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="S2y_v"        long_name="S2 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="N2x_v"        long_name="N2 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="N2y_v"        long_name="N2 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="K1x_v"        long_name="K1 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="K1y_v"        long_name="K1 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="O1x_v"        long_name="O1 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="O1y_v"        long_name="O1 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Q1x_v"        long_name="Q1 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="Q1y_v"        long_name="Q1 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="M4x_v"        long_name="M4 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="M4y_v"        long_name="M4 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="K2x_v"        long_name="K2 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="K2y_v"        long_name="K2 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="P1x_v"        long_name="P1 current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="P1y_v"        long_name="P1 current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Mfx_v"        long_name="Mf current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="Mfy_v"        long_name="Mf current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />
	         <field id="Mmx_v"        long_name="Mm current barotrope along j-axis harmonic real part "        unit="m/s"      />
	         <field id="Mmy_v"        long_name="Mm current barotrope along j-axis harmonic imaginary part "   unit="m/s"      />	 

	         <field id="M2amp_v2D"      long_name="M2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="M2phase_v2D"    long_name="M2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="S2amp_v2D"      long_name="S2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="S2phase_v2D"    long_name="S2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="N2amp_v2D"      long_name="N2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="N2phase_v2D"    long_name="N2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="K1amp_v2D"      long_name="K1 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="K1phase_v2D"    long_name="K1 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="O1amp_v2D"      long_name="O1 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="O1phase_v2D"    long_name="O1 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Q1amp_v2D"      long_name="Q1 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Q1phase_v2D"    long_name="Q1 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="M4amp_v2D"      long_name="M4 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="M4phase_v2D"    long_name="M4 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="MS4amp_v2D"      long_name="MS4 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="MS4phase_v2D"    long_name="MS4 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="MN4amp_v2D"      long_name="MN4 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="MN4phase_v2D"    long_name="MN4 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="K2amp_v2D"      long_name="K2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="K2phase_v2D"    long_name="K2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="P1amp_v2D"      long_name="P1 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="P1phase_v2D"    long_name="P1 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Mfamp_v2D"      long_name="Mf V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Mfphase_v2D"    long_name="Mf V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="Mmamp_v2D"      long_name="Mm V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="Mmphase_v2D"    long_name="Mm V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="T2amp_v2D"      long_name="T2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="T2phase_v2D"    long_name="T2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="L2amp_v2D"      long_name="L2 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="L2phase_v2D"    long_name="L2 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="S1amp_v2D"      long_name="S1 V barotropic harmonic Amplitude"                           unit="m/s"      />
	         <field id="S1phase_v2D"    long_name="S1 V barotropic harmonic Phase"                               unit="degree"   />

	         <field id="2N2amp_v2D"     long_name="2N2 V barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="2N2phase_v2D"   long_name="2N2 V barotropic harmonic Phase"                              unit="degree"   />

	         <field id="MU2amp_v2D"     long_name="MU2 V barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="MU2phase_v2D"   long_name="MU2 V barotropic harmonic Phase"                              unit="degree"   />

	         <field id="NU2amp_v2D"     long_name="NU2 V barotropic harmonic Amplitude"                          unit="m/s"      />
	         <field id="NU2phase_v2D"   long_name="NU2 V barotropic harmonic Phase"                              unit="degree"   />

	      </field_group>

	      <!-- SBC -->
	      
	      <field_group id="SBC" grid_ref="grid_T_2D" > <!-- time step automaticaly defined based on nn_fsbc -->
	         <field id="empmr"        long_name="Net Upward Water Flux"                standard_name="water_flux_out_of_sea_ice_and_sea_water"                              unit="kg/m2/s"   />
	         <field id="empbmr"       long_name="Net Upward Water Flux at pre. tstep"  standard_name="water_flux_out_of_sea_ice_and_sea_water"                              unit="kg/m2/s"   />
	         <field id="emp_oce"      long_name="Evap minus Precip over ocean"         standard_name="evap_minus_precip_over_sea_water"                                     unit="kg/m2/s"   />
	         <field id="emp_ice"      long_name="Evap minus Precip over ice"           standard_name="evap_minus_precip_over_sea_ice"                                       unit="kg/m2/s"   />
	         <field id="saltflx"      long_name="Downward salt flux"                                                                                                        unit="1e-3/m2/s" />
	         <field id="fmmflx"       long_name="Water flux due to freezing/melting"                                                                                        unit="kg/m2/s"   />
	         <field id="snowpre"      long_name="Snow precipitation"                   standard_name="snowfall_flux"                                                        unit="kg/m2/s"   />
	         <field id="runoffs"      long_name="River Runoffs"                        standard_name="water_flux_into_sea_water_from_rivers"                                unit="kg/m2/s"   />
	         <field id="precip"       long_name="Total precipitation"                  standard_name="precipitation_flux"                                                   unit="kg/m2/s"   />
	 
	         <field id="qt"           long_name="Net Downward Heat Flux"                standard_name="surface_downward_heat_flux_in_sea_water"                              unit="W/m2"                           />
	         <field id="qns"          long_name="non solar Downward Heat Flux"                                                                                               unit="W/m2"                           />
	         <field id="qsr"          long_name="Shortwave Radiation"                   standard_name="net_downward_shortwave_flux_at_sea_water_surface"                     unit="W/m2"                           />
	         <field id="qsr3d"        long_name="Shortwave Radiation 3D distribution"   standard_name="downwelling_shortwave_flux_in_sea_water"                              unit="W/m2"      grid_ref="grid_T_3D" />
	         <field id="qrp"          long_name="Surface Heat Flux: Damping"            standard_name="heat_flux_into_sea_water_due_to_newtonian_relaxation"                 unit="W/m2"                           />
	         <field id="erp"          long_name="Surface Water Flux: Damping"           standard_name="water_flux_out_of_sea_water_due_to_newtonian_relaxation"              unit="kg/m2/s"                        />
	         <field id="taum"         long_name="wind stress module"                    standard_name="magnitude_of_surface_downward_stress"                                 unit="N/m2"                           />
	         <field id="wspd"         long_name="wind speed module"                     standard_name="wind_speed"                                                           unit="m/s"                            />
	         <field id="uwnd"         long_name="u component of wind"       unit="m/s"          grid_ref="grid_U_2D"     />
	         <field id="vwnd"         long_name="v component of wind"       unit="m/s"          grid_ref="grid_V_2D"    />
	         
	         <!-- * variable relative to atmospheric pressure forcing : available with ln_apr_dyn -->
	         <field id="ssh_ib"       long_name="Inverse barometer sea surface height"  standard_name="sea_surface_height_correction_due_to_air_pressure_at_low_frequency"   unit="m"        />

	         <!-- * variable related to ice shelf forcing * -->
	         <field id="fwfisf"       long_name="Ice shelf melting"                             unit="kg/m2/s"  />
	         <field id="fwfisf3d"     long_name="Ice shelf melting"                             unit="kg/m2/s"  grid_ref="grid_T_3D" />
	         <field id="qlatisf"      long_name="Ice shelf latent heat flux"                    unit="W/m2"     />
	         <field id="qlatisf3d"    long_name="Ice shelf latent heat flux"                    unit="W/m2"     grid_ref="grid_T_3D" />
	         <field id="qhcisf"       long_name="Ice shelf heat content flux"                   unit="W/m2"     />
	         <field id="qhcisf3d"     long_name="Ice shelf heat content flux"                   unit="W/m2"     grid_ref="grid_T_3D" />
	         <field id="isfgammat"    long_name="transfert coefficient for isf (temperature) "  unit="m/s"      />
	         <field id="isfgammas"    long_name="transfert coefficient for isf (salinity)    "  unit="m/s"      />
	         <field id="stbl"         long_name="salinity in the Losh tbl                    "  unit="PSU"      />
	         <field id="ttbl"         long_name="temperature in the Losh tbl                 "  unit="C"        />
	         <field id="utbl"         long_name="zonal current in the Losh tbl at T point    "  unit="m/s"      />
	         <field id="vtbl"         long_name="merid current in the Losh tbl at T point    "  unit="m/s"      />
	         <field id="thermald"     long_name="thermal driving of ice shelf melting        "  unit="C"        />
	         <field id="tfrz"         long_name="top freezing point (used to compute melt)   "  unit="C"        />
	         <field id="tinsitu"      long_name="top insitu temperature (used to cmpt melt)  "  unit="C"        />
	         <field id="ustar"        long_name="ustar at T point used in ice shelf melting  "  unit="m/s"      />

	         <!-- *_oce variables available with ln_blk_clio or ln_blk_core -->
	         <field id="qlw_oce"      long_name="Longwave Downward Heat Flux over open ocean"  standard_name="surface_net_downward_longwave_flux"   unit="W/m2"  />
	         <field id="qsb_oce"      long_name="Sensible Downward Heat Flux over open ocean"  standard_name="surface_downward_sensible_heat_flux"  unit="W/m2"  />
	         <field id="qla_oce"      long_name="Latent Downward Heat Flux over open ocean"    standard_name="surface_downward_latent_heat_flux"    unit="W/m2"  />
	         <field id="qemp_oce"     long_name="Downward Heat Flux from E-P over open ocean"                                                       unit="W/m2"  />
	         <field id="taum_oce"     long_name="wind stress module over open ocean"           standard_name="magnitude_of_surface_downward_stress" unit="N/m2"  />

	         <!-- available key_oasis3 -->
	         <field id="snow_ao_cea"  long_name="Snow over ice-free ocean (cell average)"   standard_name="snowfall_flux"                             unit="kg/m2/s"  />
	         <field id="snow_ai_cea"  long_name="Snow over sea-ice (cell average)"          standard_name="snowfall_flux"                             unit="kg/m2/s"  />
	         <field id="subl_ai_cea"  long_name="Sublimation over sea-ice (cell average)"   standard_name="surface_snow_and_ice_sublimation_flux"     unit="kg/m2/s"  />
	         <field id="icealb_cea"   long_name="Ice albedo (cell average)"                 standard_name="sea_ice_albedo"                            unit="1"        />
	         <field id="calving_cea"  long_name="Calving"                                   standard_name="water_flux_into_sea_water_from_icebergs"   unit="kg/m2/s"  />
	         <field id="iceberg_cea"  long_name="Iceberg"                                   standard_name="water_flux_into_sea_water_from_icebergs"   unit="kg/m2/s"  />
	         <field id="iceshelf_cea" long_name="Iceshelf"                                  standard_name="water_flux_into_sea_water_from_iceshelf"   unit="kg/m2/s"  />


	         <!-- available if key_oasis3 + conservative method -->
	         <field id="rain"          long_name="Liquid precipitation"                                     standard_name="rainfall_flux"                                                                 unit="kg/m2/s"  />
	         <field id="evap_ao_cea"   long_name="Evaporation over ice-free ocean (cell average)"           standard_name="water_evaporation_flux"                                                        unit="kg/m2/s"  />
	         <field id="isnwmlt_cea"   long_name="Snow over Ice melting (cell average)"                     standard_name="surface_snow_melt_flux"                                                        unit="kg/m2/s"  />
	         <field id="fsal_virt_cea" long_name="Virtual salt flux due to ice formation (cell average)"    standard_name="virtual_salt_flux_into_sea_water_due_to_sea_ice_thermodynamics"                unit="kg/m2/s"  />
	         <field id="fsal_real_cea" long_name="Real salt flux due to ice formation (cell average)"       standard_name="downward_sea_ice_basal_salt_flux"                                              unit="kg/m2/s"  />
	         <field id="hflx_rain_cea" long_name="heat flux due to rainfall"                                standard_name="temperature_flux_due_to_rainfall_expressed_as_heat_flux_into_sea_water"        unit="W/m2"     />
	         <field id="hflx_evap_cea" long_name="heat flux due to evaporation"                             standard_name="temperature_flux_due_to_evaporation_expressed_as_heat_flux_out_of_sea_water"   unit="W/m2"     />
	         <field id="hflx_snow_cea" long_name="heat flux due to snow falling"                            standard_name="heat_flux_onto_ocean_and_ice_due_to_snow_thermodynamics"                       unit="W/m2"     />
	         <field id="hflx_snow_ai_cea" long_name="heat flux due to snow falling over ice"                standard_name="heat_flux_onto_ice_due_to_snow_thermodynamics"                                 unit="W/m2"     />
	         <field id="hflx_snow_ao_cea" long_name="heat flux due to snow falling over ice-free ocean"     standard_name="heat_flux_onto_sea_water_due_to_snow_thermodynamics"                           unit="W/m2"     />
	         <field id="hflx_ice_cea"  long_name="heat flux due to ice thermodynamics"                      standard_name="heat_flux_into_sea_water_due_to_sea_ice_thermodynamics"                        unit="W/m2"     />
	         <field id="hflx_rnf_cea"  long_name="heat flux due to runoffs"                                 standard_name="temperature_flux_due_to_runoff_expressed_as_heat_flux_into_sea_water"          unit="W/m2"     />
	         <field id="hflx_cal_cea"  long_name="heat flux due to calving"                                 standard_name="heat_flux_into_sea_water_due_to_calving"                                       unit="W/m2"     />
	         <field id="hflx_icb_cea"  long_name="heat flux due to iceberg"                                 standard_name="heat_flux_into_sea_water_due_to_icebergs"                                      unit="W/m2"     />
	         <field id="hflx_isf_cea"  long_name="heat flux due to iceshelf"                                standard_name="heat_flux_into_sea_water_due_to_iceshelf"                                      unit="W/m2"     />
	         <field id="bicemel_cea"   long_name="Rate of Melt at Sea Ice Base (cell average)"              standard_name="tendency_of_sea_ice_amount_due_to_basal_melting"                               unit="kg/m2/s"  />
	         <field id="licepro_cea"   long_name="Lateral Sea Ice Growth Rate (cell average)"               standard_name="tendency_of_sea_ice_amount_due_to_lateral_growth_of_ice_floes"                 unit="kg/m2/s"  />
	         <field id="snowmel_cea"   long_name="Snow Melt Rate (cell average)"                            standard_name="surface_snow_melt_flux"                                                        unit="kg/m2/s"  />
	         <field id="sntoice_cea"   long_name="Snow-Ice Formation Rate (cell average)"                   standard_name="tendency_of_sea_ice_amount_due_to_snow_conversion"                             unit="kg/m2/s"  />
	         <field id="ticemel_cea"   long_name="Rate of Melt at Upper Surface of Sea Ice (cell average)"  standard_name="tendency_of_sea_ice_amount_due_to_surface_melting"                             unit="kg/m2/s"  />

	         <!-- ice field (nn_ice=1)  -->
	         <field id="ice_cover"    long_name="Ice fraction"                                                 standard_name="sea_ice_area_fraction"                              unit="1"            />
	         
	         <!-- dilution -->
	         <field id="emp_x_sst"    long_name="Concentration/Dilution term on SST"                                                                                              unit="kg*degC/m2/s" />
	         <field id="emp_x_sss"    long_name="Concentration/Dilution term on SSS"                                                                                              unit="kg*1e-3/m2/s" />        
	         <field id="rnf_x_sst"    long_name="Runoff term on SST"                                                                                                              unit="kg*degC/m2/s" />
	         <field id="rnf_x_sss"    long_name="Runoff term on SSS"                                                                                                              unit="kg*1e-3/m2/s" />
	       
		 <!-- sbcssm variables -->
	         <field id="sst_m"    unit="degC" />
	         <field id="sss_m"    unit="psu"  />
	         <field id="ssu_m"    unit="m/s"  />
	         <field id="ssv_m"    unit="m/s"  />
	         <field id="ssh_m"    unit="m"    />
	         <field id="e3t_m"    unit="m"    />
	         <field id="frq_m"    unit="-"    />

	      </field_group>

	      <!-- U grid -->
	      
	      <field_group id="grid_U"   grid_ref="grid_U_2D">
	         <field id="e3u"          long_name="U-cell thickness"                                       standard_name="cell_thickness"              unit="m"          grid_ref="grid_U_3D" />
	         <field id="e3u_0"        long_name="Initial U-cell thickness"                               standard_name="ref_cell_thickness"          unit="m"          grid_ref="grid_U_3D"/>
	         <field id="utau"         long_name="Wind Stress along i-axis"                               standard_name="surface_downward_x_stress"   unit="N/m2"                            />
	         <field id="uoce"         long_name="ocean current along i-axis"                             standard_name="sea_water_x_velocity"        unit="m/s"        grid_ref="grid_U_3D" />
	         <field id="uoce_e3u"     long_name="ocean current along i-axis  (thickness weighted)"                                                   unit="m/s"        grid_ref="grid_U_3D"  > uoce * e3u </field>
	         <field id="ssu"          long_name="ocean surface current along i-axis"                                                                 unit="m/s"                             />
	         <field id="sbu"          long_name="ocean bottom current along i-axis"                                                                  unit="m/s"                             />
	         <field id="ubar"         long_name="ocean barotropic current along i-axis"                                                              unit="m/s"                             />
	         <field id="uocetr_eff"   long_name="Effective ocean transport along i-axis"                 standard_name="ocean_volume_x_transport"    unit="m3/s"       grid_ref="grid_U_3D" />
	         <field id="uocet"        long_name="ocean transport along i-axis times temperature (CRS)"                                               unit="degC*m/s"   grid_ref="grid_U_3D" />
	         <field id="uoces"        long_name="ocean transport along i-axis times salinity (CRS)"                                                  unit="1e-3*m/s"   grid_ref="grid_U_3D" />

	         <!-- u-eddy coefficients (ldftra) -->
	         <field id="ahtu_2d"      long_name=" surface u-eddy diffusivity coefficient"   unit="m2/s or m4/s" />
	         <field id="ahtu_3d"      long_name=" 3D u-EIV coefficient"                     unit="m2/s or m4/s"      grid_ref="grid_U_3D"/>
	         <field id="aeiu_2d"      long_name=" surface u-EIV coefficient"                unit="m2/s" />
	         <field id="aeiu_3d"      long_name=" 3D u-EIV coefficient"                     unit="m2/s"              grid_ref="grid_U_3D"/>

	         <!-- variables available with MLE -->
	         <field id="psiu_mle"     long_name="MLE streamfunction along i-axis"   unit="m3/s"   grid_ref="grid_U_3D" />

	         <!-- uoce_eiv: available EIV -->
	         <field id="uoce_eiv"     long_name="EIV ocean current along i-axis"   standard_name="bolus_sea_water_x_velocity"   unit="m/s"   grid_ref="grid_U_3D" />

	         <!-- uoce_eiv: available with key_trabbl -->
	         <field id="uoce_bbl"     long_name="BBL ocean current along i-axis"    unit="m/s"  />
	         <field id="ahu_bbl"      long_name="BBL diffusive flux along i-axis"   unit="m3/s" />

	         <!-- variable for ice shelves -->
	         <field id="utbl"         long_name="zonal current in the Losh tbl"     unit="m/s" />

	         <field id="u_masstr"     long_name="Ocean Mass X Transport"    standard_name="ocean_mass_x_transport"                          unit="kg/s"        grid_ref="grid_U_3D" />
	         <field id="u_masstr_vint" long_name="vertical integral of ocean eulerian mass transport along i-axis"    standard_name="vertical_integral_of_ocean_mass_x_transport"  unit="kg/s" />
	         <field id="u_heattr"     long_name="ocean eulerian heat transport along i-axis"    standard_name="ocean_heat_x_transport"                          unit="W"                                />
	         <field id="u_salttr"     long_name="ocean eulerian salt transport along i-axis"    standard_name="ocean_salt_x_transport"                          unit="1e-3*kg/s"                        />
	         <field id="uadv_heattr"  long_name="ocean advective heat transport along i-axis"    standard_name="advectice_ocean_heat_x_transport"               unit="W"                                />
	         <field id="uadv_salttr"  long_name="ocean advective salt transport along i-axis"    standard_name="advectice_ocean_salt_x_transport"               unit="1e-3*kg/s"                      />
	         <field id="ueiv_heattr"  long_name="ocean bolus heat transport along i-axis"       standard_name="ocean_heat_x_transport_due_to_bolus_advection"   unit="W"                                />
	         <field id="ueiv_salttr"  long_name="ocean bolus salt transport along i-axis"       standard_name="ocean_salt_x_transport_due_to_bolus_advection"   unit="Kg"                                />
	         <field id="ueiv_heattr3d" long_name="ocean bolus heat transport along i-axis"    standard_name="ocean_heat_x_transport_due_to_bolus_advection"   unit="W"    grid_ref="grid_U_3D" />
	         <field id="ueiv_salttr3d" long_name="ocean bolus salt transport along i-axis"    standard_name="ocean_salt_x_transport_due_to_bolus_advection"   unit="kg"   grid_ref="grid_U_3D" />
	         <field id="udiff_heattr" long_name="ocean diffusion heat transport along i-axis"   standard_name="ocean_heat_x_transport_due_to_diffusion"         unit="W"                                />
	         <field id="udiff_salttr" long_name="ocean diffusion salt transport along i-axis"   standard_name="ocean_salt_x_transport_due_to_diffusion"         unit="1e-3*kg/s"                                />
	      </field_group>
	      
	      <!-- V grid -->
	      
	      <field_group id="grid_V"   grid_ref="grid_V_2D">
	         <field id="e3v"          long_name="V-cell thickness"                                       standard_name="cell_thickness"              unit="m"          grid_ref="grid_V_3D" />
	         <field id="e3v_0"        long_name="Initial V-cell thickness"                               standard_name="ref_cell_thickness"          unit="m"          grid_ref="grid_V_3D"/>
	         <field id="vtau"         long_name="Wind Stress along j-axis"                               standard_name="surface_downward_y_stress"   unit="N/m2"                            />
	         <field id="voce"         long_name="ocean current along j-axis"                             standard_name="sea_water_y_velocity"        unit="m/s"        grid_ref="grid_V_3D" />
	         <field id="voce_e3v"     long_name="ocean current along j-axis  (thickness weighted)"                                                   unit="m/s"        grid_ref="grid_V_3D"  > voce * e3v </field>
	         <field id="ssv"          long_name="ocean surface current along j-axis"                                                                 unit="m/s"                             />
	         <field id="sbv"          long_name="ocean bottom current along j-axis"                                                                  unit="m/s"                             />
	         <field id="vbar"         long_name="ocean barotropic current along j-axis"                                                              unit="m/s"                             />
	         <field id="vocetr_eff"   long_name="Effective ocean transport along j-axis"                 standard_name="ocean_volume_y_transport"    unit="m3/s"       grid_ref="grid_V_3D" />
	         <field id="vocet"        long_name="ocean transport along j-axis times temperature (CRS)"                                               unit="degC*m/s"   grid_ref="grid_V_3D" />
	         <field id="voces"        long_name="ocean transport along j-axis times salinity (CRS)"                                                  unit="1e-3*m/s"   grid_ref="grid_V_3D" />

	         <!-- v-eddy coefficients (ldftra, ldfdyn) -->
	         <field id="ahtv_2d"      long_name=" surface v-eddy diffusivity coefficient"     unit="m2/s or (m4/s)^1/2" />
	         <field id="ahtv_3d"      long_name=" 3D v-eddy diffusivity coefficient"          unit="m2/s or (m4/s)^1/2"           grid_ref="grid_V_3D"/>
	         <field id="aeiv_2d"      long_name=" surface v-EIV coefficient"                  unit="m2/s" />
	         <field id="aeiv_3d"      long_name=" 3D v-EIV coefficient"                       unit="m2/s"                         grid_ref="grid_V_3D" />

	         <!-- variables available with MLE -->
	         <field id="psiv_mle"     long_name="MLE streamfunction along j-axis"   unit="m3/s"   grid_ref="grid_V_3D" />

	         <!-- voce_eiv: available with EIV -->
	         <field id="voce_eiv"     long_name="EIV ocean current along j-axis"   standard_name="bolus_sea_water_y_velocity"   unit="m/s"   grid_ref="grid_V_3D" />

	         <!-- voce_eiv: available with key_trabbl -->
	         <field id="voce_bbl"     long_name="BBL ocean current along j-axis"    unit="m/s"  />
	         <field id="ahv_bbl"      long_name="BBL diffusive flux along j-axis"   unit="m3/s" />

	         <!-- variable for ice shelves -->
	         <field id="vtbl"         long_name="meridional current in the Losh tbl"   unit="m/s" />

	         <!-- variables available with diaar5 -->
	         <field id="v_masstr"     long_name="ocean eulerian mass transport along j-axis"    standard_name="ocean_mass_y_transport"                          unit="kg/s"        grid_ref="grid_V_3D" />
	         <field id="v_heattr"     long_name="ocean eulerian heat transport along j-axis"    standard_name="ocean_heat_y_transport"                          unit="W"                                />
	         <field id="v_salttr"     long_name="ocean eulerian salt transport along i-axis"    standard_name="ocean_salt_y_transport"                          unit="1e-3*kg/s"                        />
	         <field id="vadv_heattr"  long_name="ocean advective heat transport along j-axis"   standard_name="advectice_ocean_heat_y_transport"                unit="W"                      />
	         <field id="vadv_salttr"  long_name="ocean advective salt transport along j-axis"   standard_name="advectice_ocean_salt_y_transport"                unit="1e-3*kg/s"              />
	         <field id="veiv_heattr"  long_name="ocean bolus heat transport along j-axis"       standard_name="ocean_heat_y_transport_due_to_bolus_advection"   unit="W"                                />
	         <field id="veiv_salttr"  long_name="ocean bolus salt transport along j-axis"       standard_name="ocean_salt_x_transport_due_to_bolus_advection"   unit="Kg"                                />
	         <field id="veiv_heattr3d" long_name="ocean bolus heat transport along j-axis"    standard_name="ocean_heat_y_transport_due_to_bolus_advection"   unit="W"    grid_ref="grid_V_3D" />
	         <field id="veiv_salttr3d" long_name="ocean bolus salt transport along j-axis"    standard_name="ocean_salt_y_transport_due_to_bolus_advection"   unit="kg"   grid_ref="grid_V_3D" />
	         <field id="vdiff_heattr" long_name="ocean diffusion heat transport along j-axis"   standard_name="ocean_heat_y_transport_due_to_diffusion"         unit="W"                                />
	         <field id="vdiff_salttr" long_name="ocean diffusion salt transport along j-axis"   standard_name="ocean_salt_y_transport_due_to_diffusion"         unit="1e-3*kg/s"                        />
	      </field_group>
	      
	      <!-- W grid -->
	      
	      <field_group id="grid_W" grid_ref="grid_W_3D">
	         <field id="e3w"          long_name="W-cell thickness"                     standard_name="cell_thickness"              unit="m"    />
	         <field id="woce"         long_name="ocean vertical velocity"              standard_name="upward_sea_water_velocity"   unit="m/s"  />
	         <field id="wocetr_eff"   long_name="effective ocean vertical transport"                                               unit="m3/s" />

	         <!-- woce_eiv: available with EIV -->
	         <field id="woce_eiv"     long_name="EIV ocean vertical velocity"   standard_name="bolus_upward_sea_water_velocity"   unit="m/s" />

	         <field id="avt"          long_name="vertical eddy diffusivity"   standard_name="ocean_vertical_heat_diffusivity"       unit="m2/s" />
	         <field id="logavt"       long_name="logarithm of vertical eddy diffusivity"   standard_name="ocean_vertical_heat_diffusivity"       unit="m2/s" />
	         <field id="avm"          long_name="vertical eddy viscosity"     standard_name="ocean_vertical_momentum_diffusivity"   unit="m2/s" />

	         <!-- avs: available with key_zdfddm -->
	         <field id="avs"          long_name="salt vertical eddy diffusivity"   standard_name="ocean_vertical_salt_diffusivity"   unit="m2/s" />
	         <field id="logavs"       long_name="logarithm of salt vertical eddy diffusivity"   standard_name="ocean_vertical_heat_diffusivity"       unit="m2/s" />

	         <!-- avt_evd and avm_evd: available with ln_zdfevd -->
	         <field id="avt_evd"      long_name="convective enhancement of vertical diffusivity"   standard_name="ocean_vertical_tracer_diffusivity_due_to_convection"     unit="m2/s" />
	         <field id="avm_evd"      long_name="convective enhancement of vertical viscosity"     standard_name="ocean_vertical_momentum_diffusivity_due_to_convection"   unit="m2/s" />

	         <!-- avt_tide: available with key_zdftmx -->
	         <field id="av_tide"      long_name="tidal vertical diffusivity"   standard_name="ocean_vertical_tracer_diffusivity_due_to_tides"   unit="m2/s" />

	         <!-- variables available with key_zdftmx_new -->
	         <field id="av_ratio"     long_name="S over T diffusivity ratio"            standard_name="salinity_over_temperature_diffusivity_ratio"                     unit="1"    />
	         <field id="av_wave"      long_name="wave-induced vertical diffusivity"     standard_name="ocean_vertical_tracer_diffusivity_due_to_internal_waves"         unit="m2/s" />
	         <field id="bflx_tmx"     long_name="wave-induced buoyancy flux"            standard_name="buoyancy_flux_due_to_internal_waves"                             unit="W/kg" />
	         <field id="pcmap_tmx"    long_name="power consumed by wave-driven mixing"  standard_name="vertically_integrated_power_consumption_by_wave_driven_mixing"   unit="W/m2"      grid_ref="grid_W_2D" />
	         <field id="emix_tmx"     long_name="power density available for mixing"    standard_name="power_available_for_mixing_from_breaking_internal_waves"         unit="W/kg" />

	         <!-- variables available with diaar5 -->   
	         <field id="w_masstr"     long_name="vertical mass transport"             standard_name="upward_ocean_mass_transport"             unit="kg/s"   />
	         <field id="w_masstr2"    long_name="square of vertical mass transport"   standard_name="square_of_upward_ocean_mass_transport"   unit="kg2/s2" />

	         <!-- aht2d and  aht2d_eiv -->
	         <field id="aht2d"        long_name="lateral eddy diffusivity"       standard_name="ocean_tracer_xy_laplacian_diffusivity"      unit="m2/s"   grid_ref="grid_W_2D" />
	         <field id="aht2d_eiv"    long_name="EIV lateral eddy diffusivity"   standard_name="ocean_tracer_bolus_laplacian_diffusivity"   unit="m2/s"   grid_ref="grid_W_2D" />

	      </field_group>
	        
	      <!-- F grid -->
	      <!-- f-eddy viscosity coefficients (ldfdyn) -->
	      <field id="ahmf_2d"      long_name=" surface f-eddy viscosity coefficient"   unit="m2/s or m4/s" />
	      <field id="ahmf_3d"      long_name=" 3D      f-eddy viscosity coefficient"   unit="m2/s or m4/s"                           grid_ref="grid_T_3D"/>

	      <field_group id="scalar"  grid_ref="grid_T_2D"  >
	         <field id="voltot"     long_name="global total volume"                          standard_name="sea_water_volume"                               unit="m3"   />
	         <field id="sshtot"     long_name="global mean ssh"                              standard_name="global_average_sea_level_change"                unit="m"    />
	         <field id="sshsteric"  long_name="global mean ssh steric"                       standard_name="global_average_steric_sea_level_change"         unit="m"    />
	         <field id="sshthster"  long_name="global mean ssh thermosteric"                 standard_name="global_average_thermosteric_sea_level_change"   unit="m"    />
	         <field id="masstot"    long_name="global total mass"                            standard_name="sea_water_mass"                                 unit="kg"   />
	         <field id="temptot"    long_name="global mean temperature"                      standard_name="sea_water_potential_temperature"                unit="degC" />
	         <field id="saltot"     long_name="global mean salinity"                         standard_name="sea_water_salinity"                             unit="1e-3" />
	         <field id="fram_trans" long_name="Sea Ice Mass Transport Through Fram Strait"   standard_name="sea_ice_transport_across_line"                  unit="kg/s" />

	      	 <!-- available with ln_diahsb -->
	         <field id="bgtemper"     long_name="drift in global mean temperature wrt timestep 1"                 standard_name="change_over_time_in_sea_water_potential_temperature"   unit="degC"     />
	         <field id="bgsaline"     long_name="drift in global mean salinity wrt timestep 1"                    standard_name="change_over_time_in_sea_water_practical_salinity"      unit="1e-3"     />
	         <field id="bgheatco"     long_name="drift in global mean heat content wrt timestep 1"                                                                                      unit="1.e20J"   />
	         <field id="bgheatfx"     long_name="drift in global mean heat flux    wrt timestep 1"                                                                                      unit="W/m2"     />
	         <field id="bgsaltco"     long_name="drift in global mean salt content wrt timestep 1"                                                                                      unit="1e-3*km3" />
	         <field id="bgvolssh"     long_name="drift in global mean ssh volume wrt timestep 1"                                                                                        unit="km3"      />
	         <field id="bgvole3t"     long_name="drift in global mean volume variation (e3t) wrt timestep 1"                                                                            unit="km3"      />
	         <field id="bgfrcvol"     long_name="global mean volume from forcing"                                                                                                       unit="km3"      />
	         <field id="bgfrctem"     long_name="global mean heat content from forcing"                                                                                                 unit="1.e20J"   />
	         <field id="bgfrchfx"     long_name="global mean heat flux from forcing"                                                                                                    unit="W/m2"     />
	         <field id="bgfrcsal"     long_name="global mean salt content from forcing"                                                                                                 unit="1e-3*km3" />
	         <field id="bgmistem"     long_name="global mean temperature error due to free surface (linssh true)"                                                                            unit="degC"     />
	         <field id="bgmissal"     long_name="global mean salinity error due to free surface (linssh true)"                                                                               unit="1e-3"     />
	      </field_group>
	  
	      <!-- variables available with key_float -->

	      <field_group id="floatvar" grid_ref="grid_T_nfloat"  operation="instant" >
	         <field id="traj_lon"      long_name="floats longitude"                                                           unit="degrees_east"  />
	         <field id="traj_lat"      long_name="floats latitude"                                                            unit="degrees_north" />
	         <field id="traj_dep"      long_name="floats depth"                                                               unit="m"             />
	         <field id="traj_temp"     long_name="floats temperature"       standard_name="sea_water_potential_temperature"   unit="degC"          />
	         <field id="traj_salt"     long_name="floats salinity"          standard_name="sea_water_practical_salinity"      unit="1e-3"          />
	         <field id="traj_dens"     long_name="floats in-situ density"   standard_name="sea_water_density"                 unit="kg/m3"         />
	         <field id="traj_group"    long_name="floats group"                                                               unit="1"             />
	      </field_group>

	      <!-- variables available with iceberg trajectories -->

	      <field_group id="icbvar" domain_ref="grid_T"  > 
	         <field id="berg_melt"          long_name="icb melt rate of icebergs"                       unit="kg/m2/s"                    />
	         <field id="berg_buoy_melt"     long_name="icb buoyancy component of iceberg melt rate"     unit="kg/m2/s"                    />
	         <field id="berg_eros_melt"     long_name="icb erosion component of iceberg melt rate"      unit="kg/m2/s"                    />
	         <field id="berg_conv_melt"     long_name="icb convective component of iceberg melt rate"   unit="kg/m2/s"                    />
	         <field id="berg_virtual_area"  long_name="icb virtual coverage by icebergs"                unit="m2"                         />
	         <field id="bits_src"           long_name="icb mass source of bergy bits"                   unit="kg/m2/s"                    />
	         <field id="bits_melt"          long_name="icb melt rate of bergy bits"                     unit="kg/m2/s"                    />
	         <field id="bits_mass"          long_name="icb bergy bit density field"                     unit="kg/m2"                      />
	         <field id="berg_mass"          long_name="icb iceberg density field"                       unit="kg/m2"                      />
	         <field id="calving"            long_name="icb calving mass input"                          unit="kg/s"                       />
	         <field id="berg_floating_melt" long_name="icb melt rate of icebergs + bits"                unit="kg/m2/s"                    />
	         <field id="berg_real_calving"  long_name="icb calving into iceberg class"                  unit="kg/s"     axis_ref="icbcla" />
	         <field id="berg_stored_ice"    long_name="icb accumulated ice mass by class"               unit="kg"       axis_ref="icbcla" />
	      </field_group>

	      <!-- Poleward transport : ptr -->     
	      <field_group id="diaptr" >  
	         <field id="zomsfglo"          long_name="Meridional Stream-Function: Global"           unit="Sv"       grid_ref="gznl_W_3D" />
	         <field id="zomsfatl"          long_name="Meridional Stream-Function: Atlantic"         unit="Sv"       grid_ref="gznl_W_3D" />
	         <field id="zomsfpac"          long_name="Meridional Stream-Function: Pacific"          unit="Sv"       grid_ref="gznl_W_3D" />
	         <field id="zomsfind"          long_name="Meridional Stream-Function: Indian"           unit="Sv"       grid_ref="gznl_W_3D" />
	         <field id="zomsfipc"          long_name="Meridional Stream-Function: Pacific+Indian"   unit="Sv"       grid_ref="gznl_W_3D" />
	         <field id="zotemglo"          long_name="Zonal Mean Temperature : Global"              unit="degree_C"     grid_ref="gznl_T_3D" />
	         <field id="zotematl"          long_name="Zonal Mean Temperature : Atlantic"            unit="degree_C"     grid_ref="gznl_T_3D" />
	         <field id="zotempac"          long_name="Zonal Mean Temperature : Pacific"             unit="degree_C"     grid_ref="gznl_T_3D" />
	         <field id="zotemind"          long_name="Zonal Mean Temperature : Indian"              unit="degree_C"     grid_ref="gznl_T_3D" />
	         <field id="zotemipc"          long_name="Zonal Mean Temperature : Pacific+Indian"      unit="degree_C"     grid_ref="gznl_T_3D" />
	         <field id="zosalglo"          long_name="Zonal Mean Salinity : Global"                 unit="0.001"     grid_ref="gznl_T_3D" />
	         <field id="zosalatl"          long_name="Zonal Mean Salinity : Atlantic"               unit="0.001"     grid_ref="gznl_T_3D" />
	         <field id="zosalpac"          long_name="Zonal Mean Salinity : Pacific"                unit="0.001"     grid_ref="gznl_T_3D" />
	         <field id="zosalind"          long_name="Zonal Mean Salinity : Indian"                 unit="0.001"     grid_ref="gznl_T_3D" />
	         <field id="zosalipc"          long_name="Zonal Mean Salinity : Pacific+Indian"         unit="0.001"     grid_ref="gznl_T_3D" />
	         <field id="zosrfglo"          long_name="Zonal Mean Surface"                           unit="m2"       grid_ref="gznl_T_3D" />
	         <field id="zosrfatl"          long_name="Zonal Mean Surface : Atlantic"                unit="m2"       grid_ref="gznl_T_3D" />
	         <field id="zosrfpac"          long_name="Zonal Mean Surface : Pacific"                 unit="m2"       grid_ref="gznl_T_3D" />
	         <field id="zosrfind"          long_name="Zonal Mean Surface : Indian"                  unit="m2"       grid_ref="gznl_T_3D" />
	         <field id="zosrfipc"          long_name="Zonal Mean Surface : Pacific+Indian"          unit="m2"       grid_ref="gznl_T_3D" />
	         <field id="sophtadv"          long_name="Advective Heat Transport"                     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtadv_atl"      long_name="Advective Heat Transport: Atlantic"           unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtadv_pac"      long_name="Advective Heat Transport: Pacific"            unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtadv_ind"      long_name="Advective Heat Transport: Indian"             unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtadv_ipc"      long_name="Advective Heat Transport: Pacific+Indian"     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtldf"          long_name="Diffusive Heat Transport"                     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtldf_atl"      long_name="Diffusive Heat Transport: Atlantic"           unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtldf_pac"      long_name="Diffusive Heat Transport: Pacific"            unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtldf_ind"      long_name="Diffusive Heat Transport: Indian"             unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtldf_ipc"      long_name="Diffusive Heat Transport: Pacific+Indian"     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtove"          long_name="Overturning Heat Transport"                     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtove_atl"      long_name="Overturning Heat Transport: Atlantic"           unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtove_pac"      long_name="Overturning Heat Transport: Pacific"            unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtove_ind"      long_name="Overturning Heat Transport: Indian"             unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtove_ipc"      long_name="Overturning Heat Transport: Pacific+Indian"     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtbtr"          long_name="Barotropic Heat Transport"                     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtbtr_atl"      long_name="Barotropic Heat Transport: Atlantic"           unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtbtr_pac"      long_name="Barotropic Heat Transport: Pacific"            unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtbtr_ind"      long_name="Barotropic Heat Transport: Indian"             unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophtbtr_ipc"      long_name="Barotropic Heat Transport: Pacific+Indian"     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophteiv"          long_name="Heat Transport from mesoscale eddy advection"                     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophteiv_atl"      long_name="Heat Transport from mesoscale eddy advection: Atlantic"           unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophteiv_pac"      long_name="Heat Transport from mesoscale eddy advection: Pacific"            unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophteiv_ind"      long_name="Heat Transport from mesoscale eddy advection: Indian"             unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sophteiv_ipc"      long_name="Heat Transport from mesoscale eddy advection: Pacific+Indian"     unit="PW"       grid_ref="gznl_T_2D" />
	         <field id="sopstadv"          long_name="Advective Salt Transport"                     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstadv_atl"      long_name="Advective Salt Transport: Atlantic"           unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstadv_pac"      long_name="Advective Salt Transport: Pacific"            unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstadv_ind"      long_name="Advective Salt Transport: Indian"             unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstadv_ipc"      long_name="Advective Salt Transport: Pacific+Indian"     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstove"          long_name="Overturning Salt Transport"                     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstove_atl"      long_name="Overturning Salt Transport: Atlantic"           unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstove_pac"      long_name="Overturning Salt Transport: Pacific"            unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstove_ind"      long_name="Overturning Salt Transport: Indian"             unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstove_ipc"      long_name="Overturning Salt Transport: Pacific+Indian"     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstbtr"          long_name="Barotropic Salt Transport"                     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstbtr_atl"      long_name="Barotropic Salt Transport: Atlantic"           unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstbtr_pac"      long_name="Barotropic Salt Transport: Pacific"            unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstbtr_ind"      long_name="Barotropic Salt Transport: Indian"             unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstbtr_ipc"      long_name="Barotropic Salt Transport: Pacific+Indian"     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstldf"          long_name="Diffusive Salt Transport"                     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstldf_atl"      long_name="Diffusive Salt Transport: Atlantic"           unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstldf_pac"      long_name="Diffusive Salt Transport: Pacific"            unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstldf_ind"      long_name="Diffusive Salt Transport: Indian"             unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopstldf_ipc"      long_name="Diffusive Salt Transport: Pacific+Indian"     unit="Giga g/s" grid_ref="gznl_T_2D" />
	         <field id="sopsteiv"          long_name="Salt Transport from mesoscale eddy advection"                     unit="Giga g/s"       grid_ref="gznl_T_2D" />
	          <field id="sopsteiv_atl"      long_name="Salt Transport from mesoscale eddy advection: Atlantic"           unit="Giga g/s"       grid_ref="gznl_T_2D" />
	         <field id="sopsteiv_pac"      long_name="Salt Transport from mesoscale eddy advection: Pacific"            unit="Giga g/s"       grid_ref="gznl_T_2D" />
	         <field id="sopsteiv_ind"      long_name="Salt Transport from mesoscale eddy advection: Indian"             unit="Giga g/s"       grid_ref="gznl_T_2D" />
	         <field id="sopsteiv_ipc"      long_name="Salt Transport from mesoscale eddy advection: Pacific+Indian"     unit="Giga g/s"       grid_ref="gznl_T_2D" />       
	      </field_group>

	    <!-- 
	============================================================================================================
	                  Physical ocean model trend diagnostics : temperature, KE, PE, momentum
	============================================================================================================
	    -->

	   <!-- variables available with ln_tra_trd -->
	   <!-- Asselin trends  calculated on odd time steps-->
	   <field_group id="trendT_odd"  grid_ref="grid_T_3D">
	      <field id="ttrd_atf"      long_name="temperature-trend: asselin time filter"       unit="degree_C/s" />
	      <field id="strd_atf"      long_name="salinity   -trend: asselin time filter"       unit="0.001/s" />
	      <!-- Thickness weighted versions: -->
	      <field id="ttrd_atf_e3t"      unit="degC/s * m"  >  ttrd_atf * e3t </field>
	      <field id="strd_atf_e3t"      unit="1e-3/s * m"  >  strd_atf * e3t </field>
	      <!-- OMIP  layer-integrated trends -->
	      <field id="ttrd_atf_li"      long_name="layer integrated heat-trend: asselin time filter "       unit="W/m^2" > ttrd_atf_e3t * 1026.0 * 3991.86795711963  </field>
	      <field id="strd_atf_li"      long_name="layer integrated salt   -trend: asselin time filter "       unit="kg/(m^2 s)" > strd_atf_e3t * 1026.0 * 0.001 </field>
	    </field_group>

	    <!-- Other trends  calculated on even time steps-->
	    <field_group id="trendT_even" grid_ref="grid_T_3D">
	       <field id="ttrd_xad"      long_name="temperature-trend: i-advection"                                                                                          unit="degC/s"                        />
	       <field id="strd_xad"      long_name="salinity   -trend: i-advection"                                                                                          unit="1e-3/s"                        />
	       <field id="ttrd_yad"      long_name="temperature-trend: j-advection"                                                                                          unit="degC/s"                        />
	       <field id="strd_yad"      long_name="salinity   -trend: j-advection"                                                                                          unit="1e-3/s"                        />
	       <field id="ttrd_zad"      long_name="temperature-trend: k-advection"                                                                                          unit="degC/s"                        />
	       <field id="strd_zad"      long_name="salinity   -trend: k-advection"                                                                                          unit="1e-3/s"                        />
	       <field id="ttrd_ad"       long_name="temperature-trend: advection"               standard_name="tendency_of_sea_water_temperature_due_to_advection"           unit="degC/s"                         > sqrt( ttrd_xad^2 + ttrd_yad^2 + ttrd_zad^2 ) </field>
	       <field id="strd_ad"       long_name="salinity   -trend: advection"               standard_name="tendency_of_sea_water_salinity_due_to_advection"              unit="1e-3/s"                         > sqrt( strd_xad^2 + strd_yad^2 + strd_zad^2 ) </field>
	       <field id="ttrd_totad"    long_name="temperature-trend: total advection"         standard_name="tendency_of_sea_water_salinity_due_to_advection"              unit="degC/s"                        />
	       <field id="strd_totad"    long_name="salinity   -trend: total advection"         standard_name="tendency_of_sea_water_salinity_due_to_advection"              unit="1e-3/s"                        />
	       <field id="ttrd_sad"      long_name="temperature-trend: surface adv. (linssh true)"                                                                                unit="degC/s"   grid_ref="grid_T_2D" />
	       <field id="strd_sad"      long_name="salinity   -trend: surface adv. (linssh true)"                                                                                unit="1e-3/s"   grid_ref="grid_T_2D" />
	       <field id="ttrd_ldf"      long_name="temperature-trend: lateral  diffusion"      standard_name="tendency_of_sea_water_temperature_due_to_horizontal_mixing"   unit="degC/s"                        />
	       <field id="strd_ldf"      long_name="salinity   -trend: lateral  diffusion"      standard_name="tendency_of_sea_water_salinity_due_to_horizontal_mixing"      unit="1e-3/s"                        />
	       <field id="ttrd_zdf"      long_name="temperature-trend: vertical diffusion"      standard_name="tendency_of_sea_water_temperature_due_to_vertical_mixing"     unit="degC/s"                        />
	       <field id="strd_zdf"      long_name="salinity   -trend: vertical diffusion"      standard_name="tendency_of_sea_water_salinity_due_to_vertical_mixing"        unit="1e-3/s"                        />
	       <field id="ttrd_evd"      long_name="temperature-trend: EVD convection"                                                                                       unit="degC/s"                        />
	       <field id="strd_evd"      long_name="salinity   -trend: EVD convection"                                                                                       unit="1e-3/s"                        />

	       <!-- ln_traldf_iso=T only (iso-neutral diffusion) -->
	       <field id="ttrd_iso"      long_name="temperature-trend: isopycnal diffusion"                             unit="degC/s" > ttrd_ldf + ttrd_zdf - ttrd_zdfp </field>
	       <field id="strd_iso"      long_name="salinity   -trend: isopycnal diffusion"                             unit="1e-3/s" > strd_ldf + strd_zdf - strd_zdfp </field>
	       <field id="ttrd_zdfp"     long_name="temperature-trend: pure vert. diffusion"   unit="degC/s" />
	       <field id="strd_zdfp"     long_name="salinity   -trend: pure vert. diffusion"   unit="1e-3/s" />

	       <!-- -->
	       <field id="ttrd_dmp"      long_name="temperature-trend: interior restoring"        unit="degC/s" />
	       <field id="strd_dmp"      long_name="salinity   -trend: interior restoring"        unit="1e-3/s" />
	       <field id="ttrd_bbl"      long_name="temperature-trend: bottom boundary layer"     unit="degC/s" />
	       <field id="strd_bbl"      long_name="salinity   -trend: bottom boundary layer"     unit="1e-3/s" />
	       <field id="ttrd_npc"      long_name="temperature-trend: non-penetrative conv."     unit="degC/s" />
	       <field id="strd_npc"      long_name="salinity   -trend: non-penetrative conv."     unit="1e-3/s" />
	       <field id="ttrd_qns"      long_name="temperature-trend: non-solar flux + runoff"   unit="degC/s" grid_ref="grid_T_2D" />
	       <field id="strd_cdt"      long_name="salinity   -trend: C/D term       + runoff"   unit="degC/s" grid_ref="grid_T_2D" />
	       <field id="ttrd_qsr"      long_name="temperature-trend: solar penetr. heating"     unit="degC/s" />
	       <field id="ttrd_bbc"      long_name="temperature-trend: geothermal heating"        unit="degC/s" />

	       <!-- Thickness weighted versions: -->
	       <field id="ttrd_xad_e3t"      unit="degC/s * m" >  ttrd_xad * e3t </field>
	       <field id="strd_xad_e3t"      unit="1e-3/s * m" >  strd_xad * e3t </field>
	       <field id="ttrd_yad_e3t"      unit="degC/s * m" >  ttrd_yad * e3t </field>
	       <field id="strd_yad_e3t"      unit="1e-3/s * m" >  strd_yad * e3t </field>
	       <field id="ttrd_zad_e3t"      unit="degC/s * m" >  ttrd_zad * e3t </field>
	       <field id="strd_zad_e3t"      unit="1e-3/s * m" >  strd_zad * e3t </field>
	       <field id="ttrd_ad_e3t"       unit="degC/s * m" >  ttrd_ad  * e3t </field>
	       <field id="strd_ad_e3t"       unit="1e-3/s * m" >  strd_ad  * e3t </field>
	       <field id="ttrd_totad_e3t"    unit="degC/s * m" >  ttrd_totad  * e3t </field>
	       <field id="strd_totad_e3t"    unit="1e-3/s * m" >  strd_totad  * e3t </field>
	       <field id="ttrd_ldf_e3t"      unit="degC/s * m" >  ttrd_ldf * e3t </field>
	       <field id="strd_ldf_e3t"      unit="1e-3/s * m" >  strd_ldf * e3t </field>
	       <field id="ttrd_zdf_e3t"      unit="degC/s * m" >  ttrd_zdf * e3t </field>
	       <field id="strd_zdf_e3t"      unit="1e-3/s * m" >  strd_zdf * e3t </field>
	       <field id="ttrd_evd_e3t"      unit="degC/s * m" >  ttrd_evd * e3t </field>
	       <field id="strd_evd_e3t"      unit="1e-3/s * m" >  strd_evd * e3t </field>

	       <!-- ln_traldf_iso=T only (iso-neutral diffusion) -->
	       <field id="ttrd_iso_e3t"      unit="degC/s * m"  >  ttrd_iso * e3t </field>
	       <field id="strd_iso_e3t"      unit="1e-3/s * m"  >  strd_iso * e3t </field>
	       <field id="ttrd_zdfp_e3t"     unit="degC/s * m"  >  ttrd_zdfp * e3t </field>
	       <field id="strd_zdfp_e3t"     unit="1e-3/s * m"  >  strd_zdfp * e3t </field>

	       <!-- -->
	       <field id="ttrd_dmp_e3t"      unit="degC/s * m"  >  ttrd_dmp * e3t </field>
	       <field id="strd_dmp_e3t"      unit="1e-3/s * m"  >  strd_dmp * e3t </field>
	       <field id="ttrd_bbl_e3t"      unit="degC/s * m"  >  ttrd_bbl * e3t </field>
	       <field id="strd_bbl_e3t"      unit="1e-3/s * m"  >  strd_bbl * e3t </field>
	       <field id="ttrd_npc_e3t"      unit="degC/s * m"  >  ttrd_npc * e3t </field>
	       <field id="strd_npc_e3t"      unit="1e-3/s * m"  >  strd_npc * e3t </field>
	       <field id="ttrd_qns_e3t"      unit="degC/s * m"  >  ttrd_qns * e3t_surf </field>
	       <field id="strd_cdt_e3t"      unit="degC/s * m"  >  strd_cdt * e3t_surf </field>
	       <field id="ttrd_qsr_e3t"      unit="degC/s * m"  >  ttrd_qsr * e3t </field>
	       <field id="ttrd_bbc_e3t"      unit="degC/s * m"  >  ttrd_bbc * e3t </field>

	       <!-- OMIP  layer-integrated trends -->
	       <field id="ttrd_totad_li"    long_name="layer integrated heat-trend : total advection"       unit="W/m^2"     > ttrd_totad_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_totad_li"    long_name="layer integrated salt   -trend : total advection"      unit="kg/(m^2 s)"    > strd_totad_e3t * 1026.0 * 0.001  </field>
	       <field id="ttrd_evd_li"      long_name="layer integrated heat-trend : EVD convection"         unit="W/m^2"    > ttrd_evd_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_evd_li"      long_name="layer integrated salt   -trend : EVD convection"      unit="kg/(m^2 s)"  > strd_evd_e3t * 1026.0 * 0.001  </field>
	       <field id="ttrd_iso_li"      long_name="layer integrated heat-trend : isopycnal diffusion"    unit="W/m^2" > ttrd_iso_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_iso_li"      long_name="layer integrated salt   -trend : isopycnal diffusion"   unit="kg/(m^2 s)" > strd_iso_e3t * 1026.0 * 0.001  </field>
	       <field id="ttrd_zdfp_li"     long_name="layer integrated heat-trend : pure vert. diffusion"   unit="W/m^2" > ttrd_zdfp_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_zdfp_li"     long_name="layer integrated salt   -trend : pure vert. diffusion"   unit="kg/(m^2 s)" > strd_zdfp_e3t * 1026.0 * 0.001  </field>
	       <field id="ttrd_qns_li"      long_name="layer integrated heat-trend : non-solar flux + runoff"   unit="W/m^2" grid_ref="grid_T_2D"> ttrd_qns_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="ttrd_qsr_li"      long_name="layer integrated heat-trend : solar flux"   unit="W/m^2"  grid_ref="grid_T_3D"> ttrd_qsr_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="ttrd_bbl_li"      long_name="layer integrated heat-trend: bottom boundary layer "     unit="W/m^2" > ttrd_bbl_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_bbl_li"      long_name="layer integrated salt   -trend: bottom boundary layer "     unit="kg/(m^2 s)" > strd_bbl_e3t * 1026.0 * 0.001  </field>
	       <field id="ttrd_evd_li"      long_name="layer integrated heat -trend: evd convection "       unit="W/m^2" >ttrd_evd_e3t * 1026.0 * 3991.86795711963  </field>
	       <field id="strd_evd_li"      long_name="layer integrated salt -trend: evd convection "       unit="kg/(m^2 s)" > strd_evd_e3t * 1026.0 * 0.001  </field>

	    </field_group>

	    <!--  Total trends calculated every time step-->
	    <field_group id="trendT" grid_ref="grid_T_3D">
	       <field id="ttrd_tot"      long_name="temperature-trend: total model trend"         unit="degC/s" />
	       <field id="strd_tot"      long_name="salinity   -trend: total model trend"         unit="1e-3/s" />
	       <!-- Thickness weighted versions: -->
	       <field id="ttrd_tot_e3t"      unit="degC/s * m"  >  ttrd_tot * e3t </field>
	       <field id="strd_tot_e3t"      unit="1e-3/s * m"  >  strd_tot * e3t </field>
	       <!-- OMIP  layer-integrated total trends -->
	       <field id="ttrd_tot_li"      long_name="layer integrated heat-trend: total model trend :"         unit="W/m^2" > ttrd_tot_e3t * 1026.0 * 3991.86795711963 </field>
	       <field id="strd_tot_li"      long_name="layer integrated salt   -trend: total model trend :"         unit="kg/(m^2 s)" > strd_tot_e3t * 1026.0 * 0.001  </field>

	       <!-- **** these trends have not been apportioned to all/even/odd ts yet **** -->
	       <!-- variables available with ln_KE_trd -->
	       <field id="ketrd_hpg"     long_name="ke-trend: hydrostatic pressure gradient"          unit="W/s^3"                        />
	       <field id="ketrd_spg"     long_name="ke-trend: surface     pressure gradient"          unit="W/s^3"                        />
	       <field id="ketrd_spgexp"  long_name="ke-trend: surface pressure gradient (explicit)"   unit="W/s^3"                        />
	       <field id="ketrd_spgflt"  long_name="ke-trend: surface pressure gradient (filter)"     unit="W/s^3"                        />
	       <field id="ssh_flt"       long_name="filtered contribution to ssh (dynspg_flt)"        unit="m"       grid_ref="grid_T_2D" />
	       <field id="w0"            long_name="surface vertical velocity"                        unit="m/s"     grid_ref="grid_T_2D" />
	       <field id="pw0_exp"       long_name="surface pressure flux due to ssh"                 unit="W/s^2"   grid_ref="grid_T_2D" />
	       <field id="pw0_flt"       long_name="surface pressure flux due to filtered ssh"        unit="W/s^2"   grid_ref="grid_T_2D" />
	       <field id="ketrd_keg"     long_name="ke-trend: KE gradient         or hor. adv."       unit="W/s^3"                        />
	       <field id="ketrd_rvo"     long_name="ke-trend: relative  vorticity or metric term"     unit="W/s^3"                        />
	       <field id="ketrd_pvo"     long_name="ke-trend: planetary vorticity"                    unit="W/s^3"                        />
	       <field id="ketrd_zad"     long_name="ke-trend: vertical  advection"                    unit="W/s^3"                        />
	       <field id="ketrd_udx"     long_name="ke-trend: U.dx[U]"                                unit="W/s^3"                        />
	       <field id="ketrd_ldf"     long_name="ke-trend: lateral   diffusion"                    unit="W/s^3"                        />
	       <field id="ketrd_zdf"     long_name="ke-trend: vertical  diffusion"                    unit="W/s^3"                        />
	       <field id="ketrd_tau"     long_name="ke-trend: wind stress "                           unit="W/s^3"   grid_ref="grid_T_2D" />
	       <field id="ketrd_bfr"     long_name="ke-trend: bottom friction (explicit)"             unit="W/s^3"                        />   
	       <field id="ketrd_bfri"    long_name="ke-trend: bottom friction (implicit)"             unit="W/s^3"                        />   
	       <field id="ketrd_atf"     long_name="ke-trend: asselin time filter trend"              unit="W/s^3"                        />  
	       <field id="ketrd_convP2K" long_name="ke-trend: conversion (potential to kinetic)"      unit="W/s^3"                        />
	       <field id="KE"            long_name="kinetic energy: u(n)*u(n+1)/2"                    unit="W/s^2"                        />   

	       <!-- variables available with ln_PE_trd -->
	       <field id="petrd_xad"     long_name="pe-trend: i-advection"                unit="W/m^3"                        />
	       <field id="petrd_yad"     long_name="pe-trend: j-advection"                unit="W/m^3"                        />
	       <field id="petrd_zad"     long_name="pe-trend: k-advection"                unit="W/m^3"                        />
	       <field id="petrd_sad"     long_name="pe-trend: surface adv. (linssh true)"      unit="W/m^3"   grid_ref="grid_T_2D" />
	       <field id="petrd_ldf"     long_name="pe-trend: lateral  diffusion"         unit="W/m^3"                        />
	       <field id="petrd_zdf"     long_name="pe-trend: vertical diffusion"         unit="W/m^3"                        />
	       <field id="petrd_zdfp"    long_name="pe-trend: pure vert. diffusion"       unit="W/m^3"                        />
	       <field id="petrd_dmp"     long_name="pe-trend: interior restoring"         unit="W/m^3"                        />
	       <field id="petrd_bbl"     long_name="pe-trend: bottom boundary layer"      unit="W/m^3"                        />
	       <field id="petrd_npc"     long_name="pe-trend: non-penetrative conv."      unit="W/m^3"                        />
	       <field id="petrd_nsr"     long_name="pe-trend: surface forcing + runoff"   unit="W/m^3"                        />
	       <field id="petrd_qsr"     long_name="pe-trend: solar penetr. heating"      unit="W/m^3"                        />
	       <field id="petrd_bbc"     long_name="pe-trend: geothermal heating"         unit="W/m^3"                        />
	       <field id="petrd_atf"     long_name="pe-trend: asselin time filter"        unit="W/m^3"                        />
	       <field id="PEanom"        long_name="potential energy anomaly"             unit="1"                            />   
	       <field id="alphaPE"       long_name="partial deriv. of PEanom wrt T"       unit="degC-1"                       />   
	       <field id="betaPE"        long_name="partial deriv. of PEanom wrt S"       unit="1e3"                          />   
	    </field_group>

	    <field_group id="trendU" grid_ref="grid_U_3D">
	       <!-- variables available with ln_dyn_trd -->
	       <field id="utrd_hpg"       long_name="i-trend: hydrostatic pressure gradient"          unit="m/s^2"                        />
	       <field id="utrd_spg"       long_name="i-trend: surface     pressure gradient"          unit="m/s^2"                        />
	       <field id="utrd_spgexp"    long_name="i-trend: surface pressure gradient (explicit)"   unit="m/s^2"                        />
	       <field id="utrd_spgflt"    long_name="i-trend: surface pressure gradient (filtered)"   unit="m/s^2"                        />
	       <field id="utrd_keg"       long_name="i-trend: KE gradient         or hor. adv."       unit="m/s^2"                        />
	       <field id="utrd_rvo"       long_name="i-trend: relative  vorticity or metric term"     unit="m/s^2"                        />
	       <field id="utrd_pvo"       long_name="i-trend: planetary vorticity"                    unit="m/s^2"                        />
	       <field id="utrd_zad"       long_name="i-trend: vertical  advection"                    unit="m/s^2"                        />
	       <field id="utrd_udx"       long_name="i-trend: U.dx[U]"                                unit="m/s^2"                        />
	       <field id="utrd_ldf"       long_name="i-trend: lateral   diffusion"                    unit="m/s^2"                        />
	       <field id="utrd_zdf"       long_name="i-trend: vertical  diffusion"                    unit="m/s^2"                        />
	       <field id="utrd_tau"       long_name="i-trend: wind stress "                           unit="m/s^2"   grid_ref="grid_U_2D" />
	       <field id="utrd_bfr"       long_name="i-trend: bottom friction (explicit)"             unit="m/s^2"                        />   
	       <field id="utrd_bfri"      long_name="i-trend: bottom friction (implicit)"             unit="m/s^2"                        />   
	       <field id="utrd_tot"       long_name="i-trend: total momentum trend before atf"        unit="m/s^2"                        />   
	       <field id="utrd_atf"       long_name="i-trend: asselin time filter trend"              unit="m/s^2"                        />   
	    </field_group>

	    <field_group id="trendV" grid_ref="grid_V_3D">
	       <!-- variables available with ln_dyn_trd -->
	       <field id="vtrd_hpg"       long_name="j-trend: hydrostatic pressure gradient"          unit="m/s^2"                        />
	       <field id="vtrd_spg"       long_name="j-trend: surface     pressure gradient"          unit="m/s^2"                        />
	       <field id="vtrd_spgexp"    long_name="j-trend: surface pressure gradient (explicit)"   unit="m/s^2"                        />
	       <field id="vtrd_spgflt"    long_name="j-trend: surface pressure gradient (filtered)"   unit="m/s^2"                        />
	       <field id="vtrd_keg"       long_name="j-trend: KE gradient         or hor. adv."       unit="m/s^2"                        />
	       <field id="vtrd_rvo"       long_name="j-trend: relative  vorticity or metric term"     unit="m/s^2"                        />
	       <field id="vtrd_pvo"       long_name="j-trend: planetary vorticity"                    unit="m/s^2"                        />
	       <field id="vtrd_zad"       long_name="j-trend: vertical  advection"                    unit="m/s^2"                        />
	       <field id="vtrd_vdy"       long_name="i-trend: V.dx[V]"                                unit="m/s^2"                        />
	       <field id="vtrd_ldf"       long_name="j-trend: lateral   diffusion"                    unit="m/s^2"                        />
	       <field id="vtrd_zdf"       long_name="j-trend: vertical  diffusion"                    unit="m/s^2"                        />
	       <field id="vtrd_tau"       long_name="j-trend: wind stress "                           unit="m/s^2"   grid_ref="grid_V_2D" />
	       <field id="vtrd_bfr"       long_name="j-trend: bottom friction (explicit)"             unit="m/s^2"                        />   
	       <field id="vtrd_bfri"      long_name="j-trend: bottom friction (implicit)"             unit="m/s^2"                        />   
	       <field id="vtrd_tot"       long_name="j-trend: total momentum trend before atf"        unit="m/s^2"                        />   
	       <field id="vtrd_atf"       long_name="j-trend: asselin time filter trend"              unit="m/s^2"                        />   
	    </field_group>


	    <!-- 
	============================================================================================================
	                                        Definitions for iodef_demo.xml
	============================================================================================================
	    -->

	     <field_group id="TRD" >
	          <field field_ref="ttrd_totad_li"   name="opottempadvect"  />
	          <field field_ref="ttrd_iso_li"     name="opottemppmdiff"  />
	          <field field_ref="ttrd_zdfp_li"    name="opottempdiff"  />
	          <field field_ref="ttrd_evd_li"     name="opottempevd" />
	          <field field_ref="strd_evd_li"     name="osaltevd" />
	          <field field_ref="ttrd_qns_li"     name="opottempqns"  />
	          <field field_ref="ttrd_qsr_li"     name="rsdoabsorb" operation="accumulate" />
	          <field field_ref="strd_totad_li"   name="osaltadvect" />
	          <field field_ref="strd_iso_li"     name="osaltpmdiff"  />
	          <field field_ref="strd_zdfp_li"    name="osaltdiff" />
	    </field_group>
	    
	    <field_group id="mooring" >
	       <field field_ref="toce"         name="thetao"   long_name="sea_water_potential_temperature"      />
	       <field field_ref="soce"         name="so"       long_name="sea_water_salinity"                   />
	       <field field_ref="uoce"         name="uo"       long_name="sea_water_x_velocity"                 />
	       <field field_ref="voce"         name="vo"       long_name="sea_water_y_velocity"                 />
	       <field field_ref="woce"         name="wo"       long_name="sea_water_z_velocity"                 />
	       <field field_ref="avt"          name="difvho"   long_name="ocean_vertical_heat_diffusivity"      />
	       <field field_ref="avm"          name="difvmo"   long_name="ocean_vertical_momentum_diffusivity"  />
	   
	       <field field_ref="sst"          name="tos"      long_name="sea_surface_temperature"                       />
	       <field field_ref="sst2"         name="tossq"    long_name="square_of_sea_surface_temperature"             />
	       <field field_ref="sstgrad"      name="tosgrad"  long_name="module_of_sea_surface_temperature_gradient"    />
	       <field field_ref="sss"          name="sos"      long_name="sea_surface_salinity"                          />
	       <field field_ref="ssh"          name="zos"      long_name="sea_surface_height_above_geoid"                />
	       <field field_ref="empmr"        name="wfo"      long_name="water_flux_into_sea_water"                     />
	       <field field_ref="qsr"          name="rsntds"   long_name="surface_net_downward_shortwave_flux"           />
	       <field field_ref="qt"           name="tohfls"   long_name="surface_net_downward_total_heat_flux"          />
	       <field field_ref="taum"                                                                                   />
	       <field field_ref="20d"                                                                                    />
	       <field field_ref="mldkz5"                                                                                 />
	       <field field_ref="mldr10_1"                                                                               />
	       <field field_ref="mldr10_3"                                                                               />
	       <field field_ref="mldr0_1"                                                                                />
	       <field field_ref="mldr0_3"                                                                                />
	       <field field_ref="mld_dt02"                                                                               />
	       <field field_ref="topthdep"                                                                               />
	       <field field_ref="pycndep"                                                                                />
	       <field field_ref="tinv"                                                                                   />
	       <field field_ref="depti"                                                                                  />
	       <field field_ref="BLT"          name="blt"      long_name="barrier_layer_thickness"                       />
	       <field field_ref="utau"         name="tauuo"    long_name="surface_downward_x_stress"                     />
	       <field field_ref="vtau"         name="tauvo"    long_name="surface_downward_y_stress"                     />
	    </field_group>

	    <field_group id="groupT" >
	       <field field_ref="toce"         name="thetao"   long_name="sea_water_potential_temperature"               />
	       <field field_ref="soce"         name="so"       long_name="sea_water_salinity"                            />
	       <field field_ref="sst"          name="tos"      long_name="sea_surface_temperature"                       />
	       <field field_ref="sst2"         name="tossq"    long_name="square_of_sea_surface_temperature"             />
	       <field field_ref="sss"          name="sos"      long_name="sea_surface_salinity"                          />
	       <field field_ref="ssh"          name="zos"      long_name="sea_surface_height_above_geoid"                />
	       <field field_ref="empmr"        name="wfo"      long_name="water_flux_into_sea_water"                     />
	       <field field_ref="qsr"          name="rsntds"   long_name="surface_net_downward_shortwave_flux"           />
	       <field field_ref="qt"           name="tohfls"   long_name="surface_net_downward_total_heat_flux"          />
	       <field field_ref="taum"                                                                                   />
	       <field field_ref="20d"                                                                                    />
	       <field field_ref="mldkz5"                                                                                 />
	       <field field_ref="mldr10_1"                                                                               />
	       <field field_ref="mldr10_3"                                                                               />
	       <field field_ref="mld_dt02"                                                                               />
	       <field field_ref="topthdep"                                                                               />
	       <field field_ref="pycndep"                                                                                />
	       <field field_ref="tinv"                                                                                   />
	       <field field_ref="depti"                                                                                  />
	       <field field_ref="BLT"          name="blt"      long_name="Barrier Layer Thickness"                       />
	    </field_group>
	    
	    <field_group id="groupU" >
	       <field field_ref="uoce"         name="uo"      long_name="sea_water_x_velocity"      />
	       <field field_ref="ssu"          name="uos"     long_name="sea_surface_x_velocity"    />
	       <field field_ref="utau"         name="tauuo"   long_name="surface_downward_x_stress" />
	    </field_group>
	    
	    <field_group id="groupV" >
	       <field field_ref="voce"         name="vo"      long_name="sea_water_y_velocity"      />
	       <field field_ref="ssv"          name="vos"     long_name="sea_surface_y_velocity"    />
	       <field field_ref="vtau"         name="tauvo"   long_name="surface_downward_y_stress" />
	    </field_group>
	    
	    <field_group id="groupW" >
	       <field field_ref="woce"         name="wo"       long_name="ocean vertical velocity"  />
	    </field_group>

	    <!-- TMB diagnostic output -->
	    <field_group  id="1h_grid_T_tmb" grid_ref="grid_T_2D" operation="instant">
	       <field id="top_temp"           name="votemper_top"  unit="degC"  />
	       <field id="mid_temp"           name="votemper_mid"  unit="degC"  />
	       <field id="bot_temp"           name="votemper_bot"  unit="degC"  />
	       <field id="top_sal"            name="vosaline_top"  unit="psu"   />
	       <field id="mid_sal"            name="vosaline_mid"  unit="psu"   />
	       <field id="bot_sal"            name="vosaline_bot"  unit="psu"   />
	       <field id="sshnmasked"         name="sossheig"      unit="m"     /> 
	    </field_group>

	    <field_group  id="1h_grid_U_tmb" grid_ref="grid_U_2D" operation="instant">
	       <field id="top_u"           name="vozocrtx_top"  unit="m/s"  />
	       <field id="mid_u"           name="vozocrtx_mid"  unit="m/s"  />
	       <field id="bot_u"           name="vozocrtx_bot"  unit="m/s"  />
	       <field id="baro_u"          name="vobtcrtx"      unit="m/s"  />
	    </field_group>

	    <field_group  id="1h_grid_V_tmb" grid_ref="grid_V_2D" operation="instant">
	       <field id="top_v"           name="vomecrty_top"  unit="m/s"  />
	       <field id="mid_v"           name="vomecrty_mid"  unit="m/s"  />
	       <field id="bot_v"           name="vomecrty_bot"  unit="m/s"  />
	       <field id="baro_v"          name="vobtcrty"      unit="m/s"  />
	    </field_group>

	    <!-- 25h diagnostic output -->
	    <field_group id="25h_grid_T" grid_ref="grid_T_3D" operation="instant">
	       <field id="temper25h"         name="potential temperature 25h mean"    unit="degC" />
	       <field id="tempis25h"         name="insitu temperature 25h mean"    unit="degC" />
	       <field id="salin25h"          name="salinity 25h mean"                 unit="psu"  />
	       <field id="ssh25h"            name="sea surface height 25h mean"  grid_ref="grid_T_2D"      unit="m"    />
	    </field_group>

	    <field_group id="25h_grid_U" grid_ref="grid_U_3D" operation="instant" >
	       <field id="vozocrtx25h"         name="i current 25h mean"    unit="m/s"   />
	    </field_group>

	    <field_group id="25h_grid_V" grid_ref="grid_V_3D" operation="instant">
	       <field id="vomecrty25h"         name="j current 25h mean"    unit="m/s"    />
	    </field_group>

	    <field_group id="25h_grid_W" grid_ref="grid_W_3D" operation="instant">
	       <field id="vomecrtz25h"         name="k current 25h mean"                 unit="m/s"      />
	       <field id="avt25h"             name="vertical diffusivity25h mean"       unit="m2/s" />
	       <field id="avm25h"              name="vertical viscosity 25h mean"        unit="m2/s" />
	       <field id="tke25h"              name="turbulent kinetic energy 25h mean" />
	       <field id="mxln25h"             name="mixing length 25h mean"             unit="m" />
	    </field_group>

	     <!-- 
	============================================================================================================
	       -->
	     <!-- output variables for my configuration (example) --> 
	 
	    <field_group id="myvarOCE" >
	       <!-- grid T --> 
	       <field field_ref="e3t"          name="e3t"      long_name="vertical scale factor"           />
	       <field field_ref="sst"          name="tos"      long_name="sea_surface_temperature"         />
	       <field field_ref="sss"          name="sos"      long_name="sea_surface_salinity"            />
	       <field field_ref="ssh"          name="zos"      long_name="sea_surface_height_above_geoid"  />
	      
	       <!-- grid U --> 
	       <field field_ref="e3u"          name="e3u"     long_name="vertical scale factor"            />
	       <field field_ref="ssu"          name="uos"     long_name="sea_surface_x_velocity"           />
	      
	       <!-- grid V --> 
	       <field field_ref="e3v"          name="e3v"     long_name="vertical scale factor"            />
	       <field field_ref="ssv"          name="vos"     long_name="sea_surface_y_velocity"           />     
	    </field_group>    

	   </field_definition>

Finally the edits to the namelist_cfg file are as follows::


	nn_itend    = 3360    !  last  time step (for dt = 6 min, 240*dt = 1 day)
	nn_date0    = 20100121 !  date at nit_0000 (format yyyymmdd) used if ln_rstart=F or (ln_rstart=T and nn_rstctl=0 or 1)

The last time step is set for 2 weeks and the start date needs to reflect the atmos weight files, in this case the 21st of Jan 2010.

The surge model flux weight files need to be renamed and the relevent day of the week needs to be added section heading and relevant lines below::

	!-----------------------------------------------------------------------
	&namsbc_usr  !   namsbc_surge   surge model fluxes
	!-----------------------------------------------------------------------

    sn_wndi     = 'EAfrica_u10'              ,       1           ,'u10',   .false.     , .false. , 'week_thu'  ,'EAfrica_u10_weights_bicubic' , '' , ''
    sn_wndj     = 'EAfrica_v10'              ,       1           ,'v10',   .false.     , .false. , 'week_thu'  ,'EAfrica_v10_weights_bicubic' , '' , ''

The file name at the ends needs to match the weight file names e.g. EAfrica_u10_weights_bicubic, the week_thu needs to be the correct day of the week. In this case the 21st of Jan is on a thursday hence thu. 

Same needs to apply to the msl weight file too section heading and relevant line below::
	
	!-----------------------------------------------------------------------
	&namsbc_apr    !   Atmospheric pressure used as ocean forcing or in bulk
	!-----------------------------------------------------------------------

	sn_apr= 'EAfrica_msl',        1         ,   'msl' ,    .false.    , .false., 'week_thu'   ,  'EAfrica_msl_weights_bicubic'      ,   ''     ,  ''


Finally the tide harmonic analysis needs to match the model runtime::

	!-----------------------------------------------------------------------
	&nam_diaharm   !   Harmonic analysis of tidal constituents ('key_diaharm')
	!-----------------------------------------------------------------------
	
	nit000_han = 1     ! First time step used for harmonic analysis
    nitend_han = 3360     ! Last time step used for harmonic analysis

A restart folder is required to write the restart file into::

	cd $EXP
	mkdir Restart_files

Now execute the model by::

	cd $EXP
	mpirun -n 4 ./opa 

This results in all 4 cores of the docker instance being ultilised, (if more are availble the processor number can be increased) however the netcdf libraries are not parallel so result in a netcdf output file for each core. Currently takes around 30 mins to run the model on my laptop for a 2 week forecast.





